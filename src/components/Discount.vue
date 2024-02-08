<template>
    <div class="discount">
        <h4> 지금 결제 시, 카페 '붉은 산호' 아메리카노 {{ per }}% 할인 쿠폰 증정!</h4>
    </div>
</template>

<script>
export default {
    name: 'DiscountBanner',
    data() {
        return {
            per : 100,
        }
    },
    /*
    과제 1) 1초마다 할인율 1%씩 감소(hint: setInterval)
    */
    mounted() {
    setInterval(() => {
        if (this.per > 10) {
            this.per--;
        } else {
            clearInterval(this.interval);   // 10이 되면 setInterval 중지
        }
    }, 1000);
  },
}
</script>

<style>

.discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  margin-top: 60px;
  border-radius: 5px;
} 

</style>
