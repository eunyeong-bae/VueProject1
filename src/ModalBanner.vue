<template>
    <div class="black-bg" v-if="isOpenModal">
        <div class="white-bg" v-if="isOpenModal">
        <img :src="products[isClicked].image" class="room-img"/>
        <h4>{{products[isClicked].title}}</h4>
        <p>{{ products[isClicked].content }}</p>
        <!-- <input @input="month = $event.target.value"/> -->
        <input v-model="month"/>
        <p>{{ month }}개월 선택함 : {{ month === 1 ? products[isClicked].price : products[isClicked].price * month }}원</p>

        <button @click="$emit('closeModal')">닫기</button>
        </div>
    </div>
</template>

<script>

export default {
    name: 'ModalBanner',
    data(){
        return{
            month: 1,
        }
    },
    watch :{
        month(a){
            if(a >= 13){
                alert('overmonth')
            }
            // else if(typeof a === 'string'){
            //     console.log(typeof a, this.month)
            //     // this.month = 1;
            //     alert('문자 입력하지마세요');
            // }
        }
    },
    props: {
        products: Array,
        isClicked: Number,
        isOpenModal: Boolean,
    }, 

    beforeUpdate(){
        if(this.month == 2){
            alert('3개월부터 입력 가능합니다.');
            this.month = 3;
        }
    }
}
</script>

<style>
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
</style>