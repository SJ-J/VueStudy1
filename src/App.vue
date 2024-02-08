<template>

  <!-- Modal Popup -->
  <div class="start" :class="{ end : modalOpen }">
    <ModalPop :rooms="rooms" :modalOpen="modalOpen" :roomId="roomId" :closePop="closePop" />
  </div>
  
<Transition name="fade">
  <ModalPop :rooms="rooms" :modalOpen="modalOpen" :roomId="roomId" :closePop="closePop" />
</Transition>

  <!-- Menu Bar -->
  <div class="menu">
    <a v-for="(menu, i) in menuName" :key="i"> {{ menu }} </a> 
    <span id="userHi" v-if="1 == 2"> 박무현 님 안녕하세요! </span>
    <span id="userHi" v-else-if="1 == 3"> 박무현5 님 안녕하세요! </span>
    <span id="userHi" v-else> 로그인 후 이용해주세요. </span>
  </div>

  <!-- Banner -->
  <DiscountBanner v-if="showDiscount == true" />


  <div :class="{ buttons : !showDiscount }">
    <button @click="sortPriceAsc"> 낮은 가격 순 </button>
    <button @click="sortPriceDesc"> 높은 가격 순 </button>
    <button @click="sortUnderFifty"> 50만 원 이하 </button>
    <button @click="sortAbc"> 가나다 순 </button>
    <button @click="sortReset"> 정렬해제 </button>
  </div>


  <!-- Products -->
  <ProductList :rooms="rooms" :openPop="openPop" :roomId="roomId" />
  <!-- <ProductList @openModal="modalOpen = true; roomId = $event" :rooms="rooms" :openPop="openPop" /> -->
  <!-- <div class="shop">
    <div v-for="(shop, i) in rooms" :key="i">
      <img :src="shop.image" class="roomImg">
      <h4 @click="openPop(i)"> {{ shop.title }} </h4>
      <p> {{ shop.price }} 원</p>
    </div>
  </div> -->
  
</template>

<script>

// components import
import roomInfo from './assets/oneroom.js'
import DiscountBanner from './components/Discount.vue';
import ModalPop from './components/Modal.vue';
import ProductList from './components/Product.vue';

export default {
  name: 'App',
    components: {
      DiscountBanner: DiscountBanner,
      ModalPop: ModalPop,
      ProductList: ProductList,
    },
  data() {
    return {  // object 형식{k:v}으로 저장
      objectData : {name: 'shin', age: 29},
      index : 0,
      reportCnt : [0, 0, 0, 0, 0, 0],
      menuName : ['Home', 'Shop', 'About'],
      rooms : roomInfo,
      roomsOrigin : [...roomInfo],  // deap copy로 오리진 데이터 보존(array, object)
      modalOpen : false,
      roomId : null,
      showDiscount : true,
    }
  },
  // mounted() {
  //   setTimeout(() => {   // 2000ms 후 실행
  //     this.showDiscount = false;
  //   }, 2000);
  // },
  methods : { // 함수는 이 자리 고정!!
    increase(index) {
      for (let i = 0; i < 1; i++) {
        this.reportCnt[index]++;
        console.log(index);
      }
    },
    openPop(roomId) {
      for (let i = 0; i < 1; i++) {
        this.modalOpen = true;
        this.roomId = roomId;
        console.log(roomId);
      }
    },
    closePop() {
      this.modalOpen = false;
    },
    sortPriceAsc() {
      this.rooms = [...this.roomsOrigin]; // copy된 data 넣어줌
      this.rooms.sort(function(a, b) {
        return a.price - b.price;
      })
    },
    sortPriceDesc() {
      this.rooms = [...this.roomsOrigin]; // copy된 data 넣어줌
      this.rooms.sort(function(a, b) {
        return b.price - a.price;
      })
    },
    sortUnderFifty() {
      // price가 500,000 미만인 데이터만 필터링하여 rooms 배열에 재할당
      this.rooms = this.rooms.filter(room => room.price < 500000);
      this.rooms.sort(function(a, b) {
          return a.price - b.price;
        })
    },
    sortAbc() {
      this.rooms = [...this.roomsOrigin]; // copy된 data 넣어줌
      this.rooms.sort(function(a, b) {
        return (a.title < b.title) ? -1 : (a.title == b.title) ? 0 : 1;
      })
    },
    sortReset() {
      this.rooms = [...this.roomsOrigin]; // copy된 data 넣어줌
      this.rooms.sort(function(a, b) {
        return a.id - b.id;
      })
    },
  },
}

</script>

<style>

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu {
  position: fixed;
  top: 0;
  background: rgb(67, 92, 124);
  padding: 15px;
  border-radius: 5px;
  width: 100%;
}
.buttons{
  padding: 10px;
  margin: 10px;
  margin-top: 60px;
  border-radius: 5px;
} 
.menu a {
  color: aliceblue;
  padding: 10px;
}
#userHi {
  color: aliceblue;
  padding: 10px;
}


</style>
