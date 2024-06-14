<template>

<DetailModal
    v-if="showModal"
    :product="selectedProduct"
    :showModal="showModal"
    @close="showModal = false"
  />

  <div class="menu">
    <a v-for="(menu, index) in menus" :key="index">{{ menu }}</a>
  </div>

  <ProductDiscount />

  <ProductCard
    v-for="product in products"
    :key="product.id"
    :product="product"
    @showModal="handleShowModal"
    @report="handleReportFake"
  />
</template>

<script>
import data from "./assets/oneroom.js";
import ProductDiscount from "./components/Discount.vue";
import DetailModal from "./modal/Modal.vue";
import ProductCard from "./components/ProductCard.vue";

// 데이터는 최상위 부모에게 만들어주는게 더 활용도가 높아진다.
// 데이터를 자식에서 부모에게 주는게 더 어렵다.

export default {
  components: {
    ProductDiscount: ProductDiscount,
    DetailModal: DetailModal,
    ProductCard: ProductCard,
  },
  name: "App",
  data() {
    return {
      showModal: false,
      selectedProduct: null,
      menus: ["Home", "Products", "About"],
      products: data.map((product) => ({ 
        ...product, flag: 0 
      })), // 신고수 초기화
    };
  },
  methods: {
    handleShowModal(product) {
      this.showModal = true;
      this.selectedProduct = product;
    },
    handleReportFake(productId) {
      const productIndex = this.products.findIndex((p) => p.id === productId);
      if (productIndex !== -1) {
        this.products[productIndex].flag++; // 인덱스를 사용하여 직접 할당
        // 또는 spread 연산자나 splice 메서드 활용
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>