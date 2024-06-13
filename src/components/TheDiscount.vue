<template>
  <div class="discount">
    <h4>지금 결제하면 {{count}}% 할인</h4> 
  </div>
</template>
<script>
  export default {
    name : 'TheDiscount',
    data(){
      return{
        count : 5,
      }
    },
    methods: {

    },
    mounted(){
      setInterval(()=>{
        if(this.count <= 0){
          return false; 
        }
        this.count--;
        console.log(this.count)
      },1000);
    }
  };

</script>
<style>
.discount{
  background: #eee;
  padding:10px;
  margin: 10px;
  border-radius: 5px;
}
</style>



