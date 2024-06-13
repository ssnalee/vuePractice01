<template>
  <transition name="fade">
    <TheModal :clickNum="clickNum" :rooms="rooms" :isShow="isShow" @closeModal="isShow=false" />
  </transition>
  <div class="menu">
    <a v-for="(a,i) in menus" :key="i">{{a}}</a>
  </div>
  <div class="btn__box">
    <button @click="priceSort()" >낮은 가격순</button>
    <button @click="priceSortReverse()" >높은 가격순</button>
    <button @click="titleSort()" >가나다순</button>
    <button @click="priceFilter()" >50만원 이하</button>
    <button @click="sortBack()">정렬 되돌리기</button>
  </div>
  <TheDiscount />
  <TheContent :room="rooms[i]" @openModal="isShow=true; clickNum= $event;" v-for="(a,i) in rooms" :key="a"/>

</template>

<script>

import data from './assets/oneroom.js';
import TheDiscount from './components/TheDiscount.vue';
import TheModal from './components/TheModal.vue';
import TheContent from "./components/TheContent.vue";
export default {
  name: 'App',
  data(){
    return{
      menus : ['Home','Product','About'],
      clickNum : 0,
      roomsOri : [...data],
      rooms : data,
      isShow : false,
      num : [0,0,0],
      showDiscount : true,
    }
  },
  methods : {
    increase(){
      this.num[0]+=1;
    },
    openModal(i){
      this.isShow=true;
      this.clickNum=i;
    },
    priceSort(){
      this.rooms = [...this.roomsOri];
      this.rooms.sort((a,b)=>{
        return a.price - b.price;
      })
    },
    priceSortReverse(){
      this.rooms = [...this.roomsOri];
      this.rooms.sort((a,b)=>{
        return b.price - a.price;
      })
    },
    titleSort(){
      this.rooms = [...this.roomsOri];
      this.rooms.sort((a,b)=>{
        if(a.title < b.title){
          return -1;
        }else if(a.title == b.title){
          return 0;
        }else{
          return 1;
        }
      })
    },
    priceFilter(){
      const filterObj = this.rooms.filter((a)=>{
        return a.price <= 500000;
      }).sort((a,b)=>{
        return a.price - b.price;
      });
      this.rooms = filterObj;
    },
    sortBack(){
      this.rooms = [...this.roomsOri];
    }
  },
  components: {
    TheDiscount,
    TheModal,
    TheContent,
  },
  // mounted(){
  //   setTimeout(()=>{
  //     this.showDiscount = false;
  //   },2000);
  // }

}
</script>

<style>
body{
  margin: 0;
}
div{
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.btn__box{
  margin: 20px;
  text-align: right;
}
.btn__box button {
  background: #fff;
  border: 1px solid #b4b4b4;
  margin: 3px;
}
.menu {
  background: darkslateblue;
  padding:15px;
  border-radius : 5px;
}
.menu a{
  color:#fff;
  padding: 10px;

}
.room__img{
  width:500px;
  margin-top:40px;
}
.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 2s;
}
.fade-enter-to {
   transform: translateY(0);
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 2s;
}
.fade-leave-to {
  opacity: 0;
}
</style>
