<template>
  <main class="p-4">
    <h1 class="m-auto text-center mb-3 mt-5">Gerenciar Pedidos</h1>
    <Dashboard />
  </main>
</template>
<script>
  import Dashboard from '../components/Dashboard.vue'
  
  export default {
    name: 'Pedidos',
    components: {
      Dashboard
    }
  }
</script>