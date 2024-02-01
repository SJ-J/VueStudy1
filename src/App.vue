<template>

<div class="modal">
  <div v-for="(detail, i) in rooms" :key="i">
    <div class="black-bg" v-if="modalOpen == true && roomId === detail.id">
      <div class="white-bg">
        <h4>{{ detail.title }}</h4>
        <div>
          {{ detail.content }}
        </div>
        <button @click="closePop">닫기</button>
      </div>
    </div>
  </div>
</div>

  <div class="menu">
    <a v-for="(menu, i) in menuName" :key="i"> {{ menu }} </a> 
    <span id="userHi" v-if="1 == 2"> 박무현 님 안녕하세요! </span>
    <span id="userHi" v-else-if="1 == 3"> 박무현5 님 안녕하세요! </span>
    <span id="userHi" v-else> 로그인 후 이용해주세요. </span>
  </div>

  <div class="shop">
    <div v-for="(shop, i) in rooms" :key="i">
      <img :src="shop.image" class="roomImg">
      <h4 @click="openPop(i)"> {{ shop.title }} </h4>
      <p> {{ shop.price }} 원</p>
      <!-- <button @click="increase(i)">허위매물신고</button> <span>신고 수 : {{ reportCnt[i] }} 건</span> -->
    </div>
  </div>
  
</template>

<script>

import roomInfo from './assets/oneroom.js'

export default {
  name: 'App',
  data() {
    return {  // object 형식{k:v}으로 저장
      index : 0,
      reportCnt : [0, 0, 0, 0, 0, 0],
      menuName : ['Home', 'Shop', 'About'],
      // products : ['백호동 원룸', '현무동 원룸', '주작동 원룸', '청룡동 원룸'],
      rooms : roomInfo,
      // 단순 String값으로 처리되기 때문에, require를 통해 import 해주면 엑박 없이 이미지 잘 뜸!!
      // imageUrl : [require('./assets/room0.jpg'), require('./assets/room1.jpg'), require('./assets/room2.jpg'), require('./assets/room3.jpg')],
      modalOpen : false,
      roomId : null,
    }
  },
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
    }
  },
  components: {
  }
}

</script>

<style>
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
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

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: rgb(67, 92, 124);
  padding: 15px;
  border-radius: 5px;
  width: 100%;
  position: fixed;
}

.menu a {
  color: aliceblue;
  padding: 10px;
}

#userHi {
  color: aliceblue;
  padding: 10px;
}

.roomImg {
  width: 400px;
  height: 250px;
  margin-top: 40px;
}

</style>
