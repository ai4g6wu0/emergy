<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div class="twselect"></div>
    <maskcomponent></maskcomponent>

  </div>
</template>


<script>


export default {
  name:'about',
  components:{
    maskcomponent:()=>import('@/components/maskcomponent.vue'),
  
  }

}
</script>  