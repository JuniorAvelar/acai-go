<template>
    <div>
        <div class="pedidos-container">
            <template v-if="pedidos.length">
            <div class="pedido" 
                v-for="pedido in filterStatus" 
                :key="pedido.id"
            >
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
                    <!-- emite um evento para o pai quando o butão é clicado passando o pedido e uma string -->
                    <button class="button-pronto" @click="$emit('updatedStatus', pedido,'Pronto' )">Pronto</button>

                    <button class="button-cancelar" @click="$emit('confirmCancel',pedido)">Cancelar</button> 
                </div>
            </div>
            </template>
            <h2 v-else>Sem pedidos no momento</h2>
        </div>
    </div>
</template>

<script>
    export default {
        name:'PedidoCard',
        props: {
            pedidos: {
                type:Array,
                required:true
            },
            filterStatus:{
                type:Array,
                required:true
            }
        }
    }
</script>

<style scoped>
    
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

/* Um único elemento que contém as duas classses  */
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