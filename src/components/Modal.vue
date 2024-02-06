<template>
    <div class="modal">
        <div v-for="(detail, i) in rooms" :key="i">
            <div class="black-bg" v-if="modalOpen == true && roomId === detail.id">
            <div class="white-bg">
                <h4>{{ detail.title }}</h4>
                <div>
                <img :src="detail.image" class="roomImg">
                <p> {{ detail.content }} </p>
                <!-- <p> <input @input="month = $event.target.value"> 개월 </p> -->
                <!-- <p> <input type="range" min="1" max="12" > 개월 </p> -->
                <p> <input v-model.number="month" autocomplete="false"> 개월 </p>
                <p> {{ month }}개월 계약 시 금액: {{ detail.price * month }} 원 </p>
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
  data() {
    return {
      month : 1,
    }
  },
  // input값에 대한 제한(month 데이터가 변할 때마다 실행되는 함수)
  /*
    과제 1) 숫자가 아닌 데이터 입력 시, alert
    과제 2) 숫자가 아닌 데이터 입력 시, month값 1로 초기화
  */
  watch: {
    month(val) {
      if( isNaN(val) ) {
        alert("숫자만 입력할 수 있습니다.");
        // this.month = val.replace(/[^0-9]/g,'1')
        // this.month = 1;
        return;
      }
    }
  },
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