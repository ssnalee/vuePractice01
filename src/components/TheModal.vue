<template>
  <div class="black_bg" v-if="isShow">
    <div class="white_bg">
      <img class="room__img" :src="rooms[clickNum].image" alt="room image" />
      <h4>{{rooms[clickNum].title}}</h4>
      <input v-model.number = "month" />
      <input type ="range" min="1" max="12" />
      <p>{{month}} 개월 선택함 : {{rooms[clickNum].price/10000 * month}}만원</p>
      <p>{{rooms[clickNum].content}}</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>    
</template>
<script>
  export default{
    name : 'TheModal',
    data(){
      return{
        month : 1,
      };
    },
    props : {
      clickNum : Number,
      rooms : Array,
      isShow : Boolean,
    },
    watch : {
      month(a){
        if(a > 13){
          alert('13 이하로만 입력하시오.')
          this.month = 13;
        }
        if(a == 2){
          alert('2당.')
        }
        if(isNaN(a) === true){
          alert('글자 ㄴㄴ')
          this.month = 1;
        }
        
      
      },
    }
  }
</script>
<style>
.black_bg{
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed;
  padding: 20px;
}
.white_bg{
  width: 100%;
  background: #fff;
  border-radius: 8px;
  padding:20px;
}
</style>