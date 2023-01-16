<template>
  <header class="bg-dark w-100 d-flex justify-content-between align-items-center p-4">
    <router-link to="/">
      <img :src="logo" :alt="alt" :title="alt" width="80" />
    </router-link>
    <div id="nav">
      <router-link to="/pedidos" class="text-white h4 text-decoration-none me-2 ms-2">Pedidos</router-link>
      <router-link to="/cardapio" class="text-white h4 text-decoration-none ms-2">Cardápio</router-link>
    </div>
  </header>
</template>
<script>
  export default {
    name: 'Header',
    props: {
      logo: String,
      alt: String
    }
  }
</script>
<style scoped>
  #nav a:hover{ color: sandybrown !important; }
  header { border-bottom: 4px solid sandybrown; }
</style>