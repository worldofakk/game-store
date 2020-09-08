<template>
  <div class="v-catalog">
    <router-link :to="{name: 'cart', params: {cart_data: CART}}">
      <div class="v-catalog__link-to-cart">
      Cart: {{CART.length}}
    </div>
    </router-link>
    
    <h1>Catalog</h1>
    <div class="v-catalog__list">
      <vCatalogItem
        v-for="product in PRODUCTS"
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
export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
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
      }
  },
  mounted() {
    this.GET_PRODUCTS_FROM_API()
  },
  data() {
    return {
      
    };
  },
  computed: {
    ...mapGetters([
        'PRODUCTS',
        'CART'
      ])
  }
};
</script>

<style lang="scss" scoped>
  .v-catalog {
    position: relative;
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
      top: 30px;
      right: 0;
      box-shadow: 0 0 8px 0 #e3e3e3;
      padding: 15px;
    }
  }

</style>
