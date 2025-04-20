<template>
    <h1>Pedidos</h1>
    <select>
      <option value="">prontos</option>
    </select>
    <div class="pedidos-container">

      <div class="pedido" v-for="pedido in pedidos" :key="pedido.id">
        <div class="peddido-header">
          <span>ID: # {{ pedido.id }}</span>
          <span>Nome: {{ pedido.nome }}</span>
          <div class="status-pedido">{{ pedido.status }}</div>
        </div>
        <div class="pedido-content">
          <span class="strong">Tamaho: <span class="text-sub"> {{ pedido.tamanho }} </span> </span>
          <span class="strong">Base: <span class="text-sub"> {{ pedido.base }} </span> </span>
          <span class="strong">Frutas: <span class="text-sub"> {{ pedido.frutas.join(', ') }} </span> </span>
          <span class="strong">Cremes: <span class="text-sub"> {{ pedido.cremes.join(', ') }}</span> </span>
          <span class="strong">Obs: <span class="text-sub">{{ pedido.observacao }} </span>  </span>
        </div>
        <div class="buttons-control">
          <button class="button-cancelar">Pronto</button>
          <button class="button-pronto">Cancelar</button>
        </div>
      </div>

    </div>

</template>

<script>
import axios from 'axios';

  export default {
    name: 'Pedidos',
    data() {
      return {
        pedidos: []
      }
    },

    methods: {
      async getPedidos(){
        const response = await axios.get('http://localhost:3000/pedidos') 
        this.pedidos = response.data
        console.log('Pedido',this.pedidos)
      }
    },

    mounted() {
      this.getPedidos()
    }
  }
</script>

<style scoped>
   h1{
    color: #200D2F;
    font-size: 3rem;
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
    height: 300px;
    /* width: auto; */
    min-width: 500px;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
    border-radius: 8px;
    padding: 20px;
  }

  .peddido-header {
    display: flex;
    justify-content: space-between;
    font-size: 20px;
    font-weight: bold;
  }

  .status-pedido {
    border: solid 1px #fff;
    width: 60px;
    height: 24px;
    font-size: 10px;

    background: #70B600;
    border-radius: 20px;
    color: #FFf;

    display: flex;
    justify-content: center;
    align-items: center;
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
  }
  
  .text-sub {
    color: #333;
    font-weight: 300;
  }

  .button-pronto ,.button-cancelar {
    height: 35px;
    width: 100px;
    border-radius: 8px;
    border: none;
    background-color: #FF0000;
    color: #fff;
    font-weight: bold;
    margin-right: 12px;
    cursor: pointer;
  }

  .button-cancelar {
    background: #70B600;
  }

</style>