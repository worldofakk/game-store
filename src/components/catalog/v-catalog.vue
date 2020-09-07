<template>
  <div>
    <h1>Catalog</h1>
    <div class="v-catalog">
      <vCatalogItem
        v-for="product in products"
        :key="product.article"
        :product_data="product"
        @sendArticleToParent="showToConsole"
      />
    </div>
  </div>
</template>

<script>
import vCatalogItem from "./v-catalog-item";
export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
  },
  methods: {
      showToConsole(data) {
          console.log(data)
      }
  },
  data() {
    return {
      products: [
        {
          image: "1.jpg",
          name: "Call of Duty",
          price: 2100,
          article: "T1",
          available: true,
          category: "Action",
        },
        {
          image: "2.jpg",
          name: "Divinity",
          price: 3150,
          article: "T2",
          available: true,
          category: "RPG",
        },
        {
          image: "3.jpg",
          name: "Prey",
          price: 4200,
          article: "T3",
          available: false,
          category: "Action",
        },
        {
          image: "4.jpg",
          name: "Dishonored",
          price: 5300,
          article: "T4",
          available: true,
          category: "Action",
        },
        {
          image: "5.jpg",
          name: "Flight Simulator",
          price: 6500,
          article: "T5",
          available: false,
          category: "Simulater",
        },
        {
          image: "6.jpg",
          name: "World of Warcraft",
          price: 8700,
          article: "T6",
          available: true,
          category: "Online RPG",
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
.v-catalog {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
}
</style>
