<template>
    <img class="room__img" :src="room.image" alt="room image" />
    <h4 class="red" @click="$emit('openModal',room.id)">{{room.title}}</h4>
    <p>{{room.price / 10000}}만원</p>
</template>
<script>
export default {
    name : 'TheContent',
    props : {
      room : Object,

    },
    methods : {
      openModal(i){
      this.isShow=true;
      this.clickNum=i;
    }
    }
}
</script>
<style>
</style>