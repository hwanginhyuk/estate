<template>
  <div class="black-bg" v-if="showModal">
    <div class="white-bg">
      <!-- modal-img 추가 및 사이즈 조정을 위한 스타일 적용 -->
      <img :src="product.image" class="modal-img" />
      <h4>{{ product.title }}</h4>
      <p>{{ product.content }}</p>
      <!-- <input @input="month = $event.target.value"> -->
      <input v-model.number="month" />
      <!-- <textarea v-model="month"></textarea>
      <select v-model="month">
        <option>1</option>
        <option>2</option>
        <option>3</option>
      </select> -->
      <!-- <input type="checkbox" v-model="month"> -->
      <p>{{ month }} 개월 : {{ product.price * month }} 원</p>
      <ProductDiscount />
      <button @click="$emit('close')">닫기</button>
    </div>
  </div>
</template>

<script>
import ProductDiscount from "../components/Discount.vue";

// 주의할점은 props는 read-only이다. 받아온거를 수정하면 안된다.
export default {
  name: "DetailModal",
  data() {
    return {
      month: 1,
    };
  },
  watch : {
    month(newMonth){
      if(newMonth > 12 || newMonth < 0){
        alert('1~12개월까지만 입력해주세요')
        this.month = 1
      }
    }
  },
  components: {
    ProductDiscount: ProductDiscount,
  },
  props: {
    // props를 통해 부모의 데이터 받기
    // type을 지정하는 이유는 디버깅을 위해서 작성한다
    product: {
      type: Object,
      required: true,
    },
    showModal: {
      // showModal prop 추가
      type: Boolean,
      required: true,
    },
  },
  methods: {
    blockProduct(id) {
      // 허위 매물 차단 로직을 구현합니다.
      // 예를 들어, 해당 상품을 목록에서 제거하거나 표시하지 않도록 처리합니다.
      this.$emit("block", id); // 부모에게 차단 이벤트 알림
    },
  },
};
</script>

<style>
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
.modal-img {
  width: 100;
  max-height: 300px; /* 이미지 최대 높이 제한 */
  object-fit: cover; /* 이미지 비율 유지 */
  margin-bottom: 20px;
}
</style>