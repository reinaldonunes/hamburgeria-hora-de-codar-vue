<template>
  <div class="container p-5">
    <div class="alert alert-warning m-auto mb-3" style="max-width:800px">
      <p class="mb-0">{{  msg }}</p>
    </div>  
  </div>
</template>
<script>
  export default {
    name: 'Messsage',
    props: {
      msg: String
    }
  }
</script>