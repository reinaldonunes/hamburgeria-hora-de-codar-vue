<template>
  <div id="banner" class="d-flex justify-content-start align-items-center p-5">
    <h1 class="text-white">Faça seu Burger</h1>
  </div>
</template>
<script>
  export default {
    name: 'Banner'
  }
</script>
<style scoped>
  #banner{
    background-image: url("/img/burger.jpg");
    background-position: 0px -400px;
    background-size:cover;
    height:600px;
    width:100%;
  }
  #banner h1{
    font-size:70px;
  }
</style>