<template>
  <div class="product">
    <div v-for="(shop, i) in rooms" :key="i">
      <img :src="shop.image" class="roomImg">
      <h4 @click="openPop(i)"> {{ shop.title }} </h4>
      <!-- <h4 @click="$emit('openPop', shop.id)"> {{ shop.title }} </h4> -->
      <p> {{ shop.price }} 원</p>
    </div>
  </div>
</template>

<script>
export default {
    name: 'ProductList',
    props: {
        openPop: Boolean,
        roomId: Number,
        rooms: Array,
    },
  computed: {
    shop() {
      // rooms에서 roomId와 일치하는 방의 정보를 반환하는 코드
      return this.rooms.find(room => room.id === this.roomId);
    },
  },
}
</script>

<style>
.roomImg {
  width: 400px;
  height: 250px;
  margin-top: 40px;
}
</style>