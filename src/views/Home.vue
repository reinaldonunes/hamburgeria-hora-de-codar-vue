<template>
  <main>
    <Banner />
    <div class="p-4">
      <h1 class="m-auto text-center mb-3 mt-5">Monte seu Burger</h1>
      <Form />
    </div>
  </main>
</template>
<script>
  import Banner from '../components/Banner.vue'
  import Form from '../components/Form.vue'

  export default {
    name: 'Home',
    components: {
      Banner,
      Form
    }
  }
</script>
