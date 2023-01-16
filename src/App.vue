<template>
  <Header :logo="logo" :alt="app_name" />
  <RouterView />
  <Footer />
</template>
<script>
  import Header from './components/Header.vue'
  import Footer from './components/Footer.vue'
  export default {
    name: 'App',
    data(){
      return{
        logo: '/img/logo.png',
        app_name: 'Monte seu Burger'
      }
    },
    components: {
      Header,
      Footer
    }
  }
</script>

<style scoped>

</style>
