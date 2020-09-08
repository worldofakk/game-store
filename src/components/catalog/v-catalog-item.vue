<template>
  <div class="v-catalog-item">
    <img 
        :src="require('../../assets/images/' + product_data.image)" 
        alt="img"
        class="v-catalog-item__img" 
    />
    <p class="v-catalog-item__name">{{ product_data.name }}</p>
    <p class="v-catalog-item__price">Price: {{ product_data.price }} UAH</p>
    <button 
        class="v-catalog-item__add-to-cart-btn btn"
        :class="{active}"
        @click="addToCart(); active=!active"
    >
        Add to cart
    </button>
  </div>
</template>

<script>
export default {
  name: "v-catalog-item",
  components: {},
  props: {
    product_data: {
      type: Object,
      default: () => {},
    },
  },
  methods: {
     addToCart() {
       this.$emit('addToCart', this.product_data)
     },
  },
  data() {
    return {
      active: false,
    }
  },
  mounted() {
        
    }
};
</script>

<style lang="scss" scoped>
.v-catalog-item {
  flex-basis: 25%;
  box-shadow: 0 0 8px 0 #e5e5e5;
  padding: 20px;
  margin-bottom: 20px;
  &__img {
      width: 200px;
      height: 250px;
  }
}
  .active {
    display: none;
  }
  
</style>
