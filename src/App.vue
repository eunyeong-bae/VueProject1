<template>
  <!-- <div class="start" :class="{end : isOpenModal}">
  </div> -->
  <Transition name="fade">
    <ModalBanner @closeModal="isOpenModal = false;" :products="products" v-bind:isClicked="isClicked" :isOpenModal="isOpenModal"/>
  </Transition>

  <div class="menu">
    <a  v-for="(a,i) in menuList" :key="i">{{ a }}</a>
  </div>

  <DiscountBanner v-if="showDiscount === true" :percent="percent"/>

  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <CardList @openModal="isOpenModal = true; isClicked= $event" v-for="(product, i) in products" :key="i" :product="product"/>


  <!-- <div>
    <img src="./assets/room0.jpg" class="room-img" />
    <h4 @click="isOpenModal = true">{{ products[0] }}</h4>
    <p>50 만원</p>
    <button v-on:click="increase(0)">허위매물신고</button> 
    <span>신고수 : {{ 신고수[0] }}</span>
  </div> -->
  <!-- <div>
    <img src="./assets/room1.jpg" class="room-img"/>
    <h4>{{ products[1] }}</h4>
    <p>50 만원</p>
    <button @click="increase(1)">허위매물신고</button> <span>신고수: {{ 신고수[1] }}</span>
  </div>
  <div>
    <img src="./assets/room2.jpg" class="room-img"/>
    <h4>{{ products[2] }}</h4>
    <p>50 만원</p>
    <button @click="increase(2)">허위매물신고</button> <span>신고수: {{ 신고수[2] }}</span>
  </div> -->

</template>

<script>
import data from './assets/oneroom.js';
import DiscountBanner from './DiscountBanner.vue';
import ModalBanner from './ModalBanner.vue';
import CardList from './CardList.vue';

export default {
  name: 'App',
  data(){
    return {
      percent: 30,
      showDiscount : true,
      originProducts: [...data],
      isClicked: 0,
      isOpenModal: false,
      신고수: [0,0,0],
      menuList: ['Home','Shop','About'],
      products: data,
    }
  },
  methods: {
    increase(value){
      console.log("clicked:",value)
      this.신고수[value]++;
    },
    sortBack(){
      this.products = [...this.originProducts];
    },
    priceSort(){
      this.products.sort(function(a,b){
        return a.price - b.price;
      })
    },
  },

  mounted(){
    setInterval(()=>{
      if(this.percent === 0){
        this.showDiscount = false;
        return;
      }
      this.percent -= 1;

    }, 1000)
  },

  components: {
    DiscountBanner: DiscountBanner,
    ModalBanner,
    CardList,
  }
}
</script>

<style>
.fade-leave-from{
  opacity: 1
}
.fade-leave-to{
  opacity: 0;
}

.fade-enter-from{
  transform: translateY(-1000px);
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  transform: translateY(0px);
}
/* .start {
  opacity: 0;
  transition: all 1s;
}
.end{
  opacity: 1; */
/* } */

body{
  margin: 0;
}
div{
  box-sizing: border-box;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

</style>
