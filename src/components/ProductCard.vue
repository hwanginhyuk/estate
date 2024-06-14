<template>
  <div>
    <img :src="product.image" class="room-img" />
    <h4 @click="$emit('showModal', product)">
      {{ product.title }}
    </h4>
    <p>{{ product.price }} 원</p>
    <button @click="reportFake">허위매물신고</button>
    <span>신고수 : {{ product.flag }}</span>
  </div>
</template>

<script>
// props로 보낸 데이터는 수정금지
// 커스텀 이벤트를 사용하여 데이터를 변환시킨다
// $emit('변수명', 데이터)로 부모에게 메세지를 보낼 수 있다.
export default {
  name: "ProductCard",
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  emits: ["showModal", "report"],
  methods: {
    reportFake() {
      this.$emit("report", this.product.id);
    },
  },
};
</script>

<style>
.room-img {
  width: 100%;
  max-width: 300px;
  height: auto;
  margin-top: 40px;
}
</style>
<!-- 
이벤트 버블링 현상이란? 
자식 컴포넌트에서 발생한 이벤트가 부모 컴포넌트로 전파되어 부모 컴포넌트의 이벤트 핸들러도 실행되는 현상이다.
해결방법으로는 .stop 수식어를 사용하는 경우 혹은
$emit메서드를 활용하여 커스텀 이벤트를 발생시키고, 부모 컴포넌트에서 해당 이벤트를 수신하여 처리한다.
-->