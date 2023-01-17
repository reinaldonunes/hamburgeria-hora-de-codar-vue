<template>
  <main class="p-4">
    <h1 class="m-auto text-center mb-3 mt-5">Cardápio</h1>
    <div class="mt-4 container mb-5" v-if="paes">
      <h2 class="text-secondary">Opções de Pães</h2>
      <div class="d-flex w-100 text-center justify-content-between align-items-center">
        <div class="card bg-light p-4 w-100 m-1" v-for="pao in paes" :key="pao.id">
          <p class="mb-0">{{ pao.tipo }}</p>
        </div>
      </div>
    </div>

    <div class="mt-4 container mb-5" v-if="carnes">
      <h2 class="text-secondary">Opções de Carnes</h2>
      <div class="d-flex w-100 text-center justify-content-between align-items-center">
        <div class="card bg-light p-4 w-100 m-1" v-for="carne in carnes" :key="carne.id">
          <p class="mb-0">{{ carne.tipo }}</p>
        </div>
      </div>
    </div>

    <div class="mt-4 container mb-5" v-if="opcionaisdata">
      <h2 class="text-secondary">Opções de Opcionais</h2>
      <div class="d-flex w-100 text-center justify-content-between align-items-center">
        <div class="card bg-light p-4 w-100 m-1" v-for="opcional in opcionaisdata" :key="opcional.id">
          <p class="mb-0">{{ opcional.tipo }}</p>
        </div>
      </div>
    </div>
  </main>
</template>
<script>
  export default {
    name: 'Pedidos',
    data(){
      return{
        paes: null,
        carnes: null,
        opcionaisdata:null
      }
    },

    methods: {
      async getCardapio() {
        const req = await fetch("http://localhost:3000/ingredientes")
        const data = await req.json()

        this.paes = data.paes
        this.carnes = data.carnes
        this.opcionaisdata = data.opcionais
      },
    },

    mounted(){
      this.getCardapio()
    }
  }
</script>