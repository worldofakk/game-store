<template>
  <div class="v-catalog">
    <router-link :to="{name: 'cart', params: {cart_data: CART}}">
      <div class="v-catalog__link-to-cart">
      Cart: {{CART.length}}
    </div>
    </router-link>
      <h1>Catalog</h1>
    <div class="filters">
      <vSelect
        :selected="selected"
        :options="categories"
        @select="sortByCategories"
      />
      <div class="range-slider">
        <input 
          type="range" 
          min="0" 
          max="9000" 
          step="10"
          v-model.number="minPrice"
          @change="setRangeSldiers"
        >
        <input 
          type="range" 
          min="0" 
          max="9000" 
          step="10" 
          v-model.number="maxPrice"
          @change="setRangeSldiers"
        >
        <div class="range-values">
          <p class="min">{{minPrice}}</p>
          <p class="max">{{maxPrice}}</p>
        </div>
      </div>
    </div>
    <div class="v-catalog__list">
      <vCatalogItem
        v-for="product in filteredProducts"
        :key="product.article"
        :product_data="product"
        @addToCart="addToCart"
      />
    </div>
  </div>
</template>

<script>
import vCatalogItem from "./v-catalog-item";
import {mapActions, mapGetters} from 'vuex'
import vSelect from '../v-select';
export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
    vSelect
  },
  methods: {
      ...mapActions([
        'GET_PRODUCTS_FROM_API',
        'ADD_TO_CART'
      ]),
      addToCart(data) {
        this.ADD_TO_CART(data)
      },
      disabledCartButton() {
        console.log('kek')
      },
      sortByCategories(category) {
        let self = this
        this.sortedProducts = [...this.PRODUCTS]
        this.sortedProducts = this.sortedProducts.filter(function(item) {
          return item.price >=self.minPrice && item.price <= self.maxPrice
        })
        if (category) {
          this.sortedProducts = this.sortedProducts.filter(function(e) {
          self.selected = category.name
          return e.category === category.name
        })
        }
      },
      setRangeSldiers() {
        if (this.minPrice > this.maxPrice) {
          let temp = this.maxPrice
          this.maxPrice = this.minPrice
          this.minPrice = temp
        }
        this.sortByCategories()
      }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API(),
    this.sortByCategories()
  },
  data() {
    return {
      categories: [
        {name: 'All', value: 'All'},
        {name: 'RPG', value: 'RPG'},
        {name: 'Action', value: 'Action'},
        {name: 'Simulater', value: 'Simulater'},
        {name: 'Online RPG', value: 'Online RPG'}
      ],
      selected: 'All',
      sortedProducts: [],
      minPrice: 0,
      maxPrice: 9000
    };
  },
  computed: {
    ...mapGetters([
        'PRODUCTS',
        'CART',
        'IS_DESKTOP'
      ]),
      filteredProducts() {
        if (this.sortedProducts.length) {
          return this.sortedProducts
        } else {
          return this.PRODUCTS
        }
      }
  }
};
</script>

<style lang="scss" scoped>
  .v-catalog {
    padding-top: 30px;
    &__list {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      margin-top: 30px;
    }
    &__link-to-cart {
      position: absolute;
      right: 0;
      box-shadow: 0 0 8px 0 #e3e3e3;
      padding: 15px;
    }
  }
  .filters {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .range-slider {
    width: 200px;
    margin-top: 10px;
    text-align: center;
    position: relative;
  }
  .range-slider svg, .range-slider input[type=range] {
    position: absolute;
    left: 0;
    bottom: 0;
  }
  input[type=range]::-webkit-slider-thumb {
    z-index: 2;
    position: relative;
    top: 2px;
    margin-top: -7px;
  }
  input[type=range]::-webkit-slider-runnable-track {
    background: #419ae9;
    border-radius: 15px;
  }
  .range-values {
    position: absolute;
    .min {
      position: absolute;
      left: -37px;
      top: -13px;
    }
    .max {
      position: absolute;
      left: 130px;
      top: -13px;
    }
  }

</style>
