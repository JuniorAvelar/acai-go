<template>
    <mensagem v-show="msg" :msg="msg"/>
    <h1>Pedidos</h1>
    <select class="select-status">
      <option  v-for="status in statusApi" :key="status.id" :value="status.nome">{{ status.nome }}</option>
    </select>
    <div class="pedidos-container">

     <template v-if="pedidos.length">
      <div class="pedido" v-for="pedido in pedidos" :key="pedido.id">
        <div class="peddido-header">
          <span>ID: #{{ pedido.id }}</span>
          <span>Nome: {{ pedido.nome }}</span>
          <!-- Container que exibe o status do pedido com classes dinâmicas -->
          <div :class="['status-pedido ', pedido.status]"> {{ pedido.status }}</div>
        </div>
        <div class="pedido-content">
          <span class="strong">Tamaho: <span class="text-sub"> {{ pedido.tamanho }} </span> </span>
          <span class="strong">Base: <span class="text-sub"> {{ pedido.base }} </span> </span>
          <span class="strong">Frutas: <span class="text-sub"> {{ pedido.frutas.join(', ') }} </span> </span>
          <span class="strong">Cremes: <span class="text-sub"> {{ pedido.cremes.join(', ') }}</span> </span>
          <span v-if="pedido.observacao.length" class="strong">Obs: <span class="text-sub">{{ pedido.observacao }} </span>  </span>
        </div>
        <div class="buttons-control">
          <button class="button-pronto" @click="updatedStatus(pedido, 'Pronto' )">Pronto</button>
          <button class="button-cancelar" @click="cancelarPedido(pedido)">Cancelar</button> 
        </div>
      </div>
     </template>
     <h2 v-else>Sem pedidos no momento</h2>

    </div>
</template>

<script>
import axios from 'axios';
import Mensagem from '@/components/Mensagem.vue';

  export default {
    name: 'Pedidos',
    components: {
      Mensagem,
    },

    data() {
      return {
        pedidos: [],

        statusApi:[],

        msg:'',
      }
    },

    methods: {
      async getPedidos(){
        const response = await axios.get('http://localhost:3000/pedidos') 
        this.pedidos = response.data
        console.log('Pedido',this.pedidos)
      },

      async getStatus() {
        const response = await axios.get('http://localhost:3000/status')
        this.statusApi = response.data
        this.status = this.statusApi[0].nome
      },

      async updatedStatus(pedido , novoStatus) {
        try {
          // Envia requisição PATCH para a API, alterando apenas o campo `status` do pedido especificado
          await axios.patch(`http://localhost:3000/pedidos/${pedido.id}`, {
            status:novoStatus
          })
          this.getPedidos()
          this.getStatus()

        } catch (error) {
          console.log("Erro ao atulizar o pedido" , error)
        }
      },  

//         
      async cancelarPedido(pedido) {
        try {
          // Envia requisição DELETE para a API, removendo o pedido com o ID informado
          await axios.delete(`http://localhost:3000/pedidos/${pedido.id}`)
          // atualiza os pedidos na tela 
          this.getPedidos()
          this.getStatus()
        } catch (error) {
          console.log('Erro ao apagar o pedido' , error)
        }

        this.msg = "Pedido cancelado com sucesso!"

        setTimeout(() => {
          this.msg = ""
        } ,3000)
      }
    },

    mounted() {
      this.getPedidos()
      this.getStatus()
    }
  }
</script>

<style scoped>
   h1{
    color: #200D2F;
    font-size: 3rem;
    margin-left: 40px;
  }

  .select-status {
    padding: 5px;
    font-size: 14px;
    border-radius: 8px;
    width: 150px;
    border: none;
    background: #D9D9D9;
    margin-left: 40px;
  }


  .pedidos-container {
    padding: 25px;
    display: flex;
  
    justify-content: center;
    flex-wrap: wrap;
    gap: 20px;
  }

  .pedido {
    height: 400px;
    width: 460px;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
    border-radius: 8px;
    padding: 30px 20px;

    display: flex;
    flex-direction: column;
    justify-content: space-between;

  }

  .peddido-header {
    display: flex;
    justify-content: space-between;
    align-items: center;

    font-size: 20px;
    font-weight: bold;
    border-bottom:solid 2px #200D2F;
  }

  .status-pedido {
    border: solid 1px #fff;
    width: 70px;
    height: 24px;
    font-size: 10px;
    padding: 10px;

    background: #70B600;
    border-radius: 20px;
    color: #FFf;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  .status-pedido.Solicitado {
    background: #e5b413;
    color: #333;
  }

  .status-pedido.Pronto {
    background: #0de643;
    color: #ffffff;
  }
  
  .pedido-content {
    display: flex;
    flex-direction: column;
    margin-top: 1rem;
    margin-bottom: 2rem;
    gap: 10px;
  }

  .strong {
    font-weight: 600 ;
    font-size: 16px;
    width: 100%;
  }
  
  .text-sub {
    color: #000000;
    font-weight: 300;
  }

  .button-pronto ,.button-cancelar {
    height: 35px;
    width: 100px;
    border-radius: 8px;
    border: none;
    background-color: #059c2b;
    color: #fff;
    font-weight: bold;
    margin-right: 12px;
    cursor: pointer;
  }

  .button-pronto:hover ,.button-cancelar:hover {
    opacity: 0.8;
  }

  .button-cancelar {
    background: #db1c1c;
  }

</style>