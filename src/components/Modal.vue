<template>
    <div class="modal">
        <div v-for="(detail, i) in rooms" :key="i">
            <div class="black-bg" v-if="modalOpen == true && roomId === detail.id">
            <div class="white-bg">
                <h4>{{ detail.title }}</h4>
                <div>
                <img :src="detail.image" class="roomImg">
                <p> {{ detail.price }} 원</p>
                <p> {{ detail.content }} </p>
                </div>
                <button @click="closePop">닫기</button>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ModalPop',
  props: {
    modalOpen: Boolean,
    roomId: Number,
    closePop: Function,
    rooms: Array,
  },
  computed: {
    detail() {
      // rooms에서 roomId와 일치하는 방의 정보를 반환하는 코드
      return this.rooms.find(room => room.id === this.roomId);
    },
  },
};
</script>

<style>
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
  margin-top: 40px;
}
</style>