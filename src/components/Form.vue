<template>
  <div>
    <Message :msg="msg" v-if="msg" />
    <form class="container mb-5" style="max-width:800px" @submit="createBurger">
      <div class="w-100 mb-3 left-detail">
        <label class="form-label w-100">Nome do Cliente:</label>
        <input type="text" name="nome" class="form-control mb-2" v-model="nome" placeholder="Digite o seu nome"/>
      </div>

      <div class="w-100 mb-3  left-detail">
        <label class="form-label w-100">Escolha o Pão:</label>
        <select name="pao" v-model="pao" class="form-select">
          <option :value="null">Selecione o Pão</option>
          <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
        </select>
      </div>

      <div class="w-100 mb-3  left-detail">
        <label class="form-label w-100">Escolha a Carne:</label>
        <select name="carne" v-model="carne" class="form-select">
          <option :value="null" selected>Selecione a Carne</option>
          <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
        </select>
      </div>

      <div class="w-100 mb-3 left-detail">
        <label class="form-label w-100">Selecione os opcionais:</label>
        <div class="input-group">
          <span class="d-flex align-items-center me-4" v-for="opcional in opcionaisdata" :key="opcional.id">
            <input class="form-check-input mt-0" type="checkbox" :value="opcional.tipo" v-model="opcionais" name="opcionais" />
            &nbsp;&nbsp;{{  opcional.tipo }}
          </span>
        </div>
      </div>

      <input type="submit" class="btn btn-primary btn-lg" value="Montar" />
    </form>
  </div>
</template>
<script>
  import Message from '../components/Message.vue'

  export default {
    name: 'Form',
    components: { Message },
    data(){
      return{
        paes: null,
        carnes: null,
        opcionaisdata: null,
        nome: null,
        pao:null,
        carne: null,
        opcionais: [],
        msg: null,
        status: "Solicitado",
      }
    },

    methods: {
      async getIngredientes(){
        const req = await fetch("http://localhost:3000/ingredientes")
        const data = await req.json()

        this.paes = data.paes
        this.carnes = data.carnes
        this.opcionaisdata = data.opcionais
      },

      async createBurger(e){
        e.preventDefault()

        const order = {
          nome: this.nome,
          carne: this.carne,
          pao: this.pao,
          opcionais: Array.from(this.opcionais),
          status: "Solicitado"
        }

        const orderJson = JSON.stringify(order)
        
        const req = await fetch("http://localhost:3000/burgers", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: orderJson
        })

        const res = await req.json()

        this.msg = `Pedido nº ${ res.id } realizado com sucesso.`
        setTimeout(() => this.msg = "", 1500)

        this.nome = null,
        this.carne = null,
        this.pao = null,
        this.opcionais = null
      }
    },
    
    mounted(){
      this.getIngredientes()
    }

  }
</script>
<style scoped>
.form-control{
    height:55px !important;
  }
  .left-detail label{
    border-left:4px solid sandybrown;
    padding-left:10px;
  }
</style>