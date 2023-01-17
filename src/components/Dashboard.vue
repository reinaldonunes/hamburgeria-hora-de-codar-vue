<template>
  <div class="container p-4">
    <Message :msg="msg" v-if="msg" />
    <table class="table table-striped align-middle">
      <thead>
        <tr class="bg-dark text-white">
          <th scope="col">Pedido nº</th>
          <th scope="col">Cliente</th>
          <th scope="col">Pão</th>
          <th scope="col">Carne</th>
          <th scope="col">Opcionais</th>
          <th scope="col">Status</th>
          <th scope="col"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="order in orders" :key="order.id">
          <th scope="row">{{  order.id }}</th>
          <td>{{ order.nome }}</td>
          <td>{{ order.pao }}</td>
          <td>{{ order.carne }}</td>
          <td>
            <ul v-if="order.opcionais" >
              <li v-for="opcional in order.opcionais" :key="opcional.id" class="mb-2">
                {{  opcional }}
              </li>
            </ul>
          </td>
          <td>
            <select class="form-select" @change="updateOrder($event, order.id)">
              <option value="">Status</option>
              <option v-for="opt in status" :key="opt.id" :value="opt.tipo" :selected="order.status === opt.tipo">{{  opt.tipo }}</option>
            </select>
          </td>
          <td class="text-center">
            <button class="btn btn-danger" @click="cancelOrder(order.id)">Cancelar pedido</button>
          </td>
        </tr>
        
      </tbody>
    </table>
  </div>
</template>
<script>
  import Message from '../components/Message.vue'

  export default {
    name: 'Dashboard',
    components: {
      Message
    }, 
    data(){
      return{
        orders: [],
        status: [],
        msg: null
      }
    },

    methods: {
      async getStatus(){
        const req = await fetch("http://localhost:3000/status")
        const data = await req.json()

        this.status = data
      },

      async getOrders(){
        const req = await fetch("http://localhost:3000/burgers")
        const data = await req.json()

        this.orders = data
      },

      async cancelOrder(idOrder){
        if(confirm("Deseja mesmo cancelar este pedido?")){
          const req = await fetch(`http://localhost:3000/burgers/${idOrder}`, {
            method: "DELETE"
          })

          this.msg = "Pedido cancelado com sucesso."
          setTimeout(() => this.msg = "", 1500)

          this.getOrders()
        }
      },

      async updateOrder(event, id){
        const option = event.target.value

        const dataJson = JSON.stringify({ status: option })

        const req = await fetch(`http://localhost:3000/burgers/${id}`,{
          method: 'PATCH',
          headers: { "Content-Type": "application/json"},
          body: dataJson
        })

        this.msg = `Pedido nº ${id} atualizado com sucesso.`
        setTimeout(() => this.msg = "", 1500)


      },

    },

    mounted() {
      this.getOrders();
      this.getStatus();
    }
  }
</script>