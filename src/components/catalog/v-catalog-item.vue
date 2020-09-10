<template>
  <div class="v-catalog-item">

    <vPopUp
      v-if="isInfoPopUpVisible"
      @closePopUp="closePopUp"
      rightBtnTitle="Add to cart"
      :popupTitle="product_data.name"
      @rightBtnAction="addToCart"
    >
    <img 
      :src="require('../../assets/images/' + product_data.image)" 
      alt="img"
      class="v-catalog-item__img" 
    />
    <div>
      <p class="v-catalog-item__price">Price: {{ product_data.price }} UAH</p>
      <p class="v-catalog-item__price">{{product_data.category}}</p>
      <p>Самая лучшая игра!</p>
    </div>
    </vPopUp>
      



    <img 
        :src="require('../../assets/images/' + product_data.image)" 
        alt="img"
        class="v-catalog-item__img" 
    />
    <p class="v-catalog-item__name">{{ product_data.name }}</p>
    <p class="v-catalog-item__price">Price: {{ product_data.price }} UAH</p>
    <div class="button-block">
      <button
      class="v-catalog-item__show-info btn btn-info"
      @click="showPopupInfo"
    >
      info
    </button>
    <button 
        class="v-catalog-item__add-to-cart-btn btn"
        :class="{active}"
        @click="addToCart(); active=!active"
    >
        Add to cart
    </button>
    </div>
  </div>
</template>

<script>
import vPopUp from '../pop-up/v-popup'
export default {
  name: "v-catalog-item",
  components: {
    vPopUp
  },
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
     showPopupInfo() {
       this.isInfoPopUpVisible = true
     },
     closePopUp() {
       this.isInfoPopUpVisible = false
     }
  },
  data() {
    return {
      active: false,
      isInfoPopUpVisible: false
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
.button-block {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
  
</style>
