<template>
  <div class="v-cart">
    <router-link :to="{name: 'catalog'}">
      <div class="v-cart__link-to-cart">Back to Catalog</div>
    </router-link>
    <h1>Cart</h1>
    <p 
        class="v-cart__text" v-if="!cart_data.length"
    >
        There are no products in cart...
    </p>
    <vCartItem
      v-for="(item, index) in cart_data"
      :key="item.article"
      :cart_item_data="item"
      @deleteFromCart="deleteFromCart(index)"
    />
  </div>
</template>

<script>
import vCartItem from "./v-cart-item.vue"
import { mapActions } from "vuex"
export default {
  name: "v-cart",
  components: {
    vCartItem,
  },
  computed: {},
  props: {
    cart_data: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    ...mapActions(["DELETE_FROM_CART"]),
    deleteFromCart(index) {
      this.DELETE_FROM_CART(index)
    },
  },
}
</script>

<style lang="scss" scoped>
.v-cart {
  position: relative;
  padding-top: 30px;
  &__link-to-cart {
    position: absolute;
    top: 30px;
    right: 0;
    box-shadow: 0 0 8px 0 #e3e3e3;
    padding: 15px;
  }
  &__text {
      margin-top: 100px;
      font-size: 1.5rem;
  }
}
</style>