<template>
    <mensagem v-show="msg" :msg="msg"/>
    <h1>Pedidos</h1>

    <SelectStatus
     :statusApi="statusApi"
      v-model:statusSelecionado="statusSelecionado"
    />
    <PedidoCard :pedidos="pedidos" 
      :filterStatus="filterStatus"
      @updatedStatus="updatedStatus" 
      @cancelarPedido="cancelarPedido" 
     />
</template>

<script>
import axios from 'axios';
import Mensagem from '@/components/Mensagem.vue';
import SelectStatus from './SelectStatus.vue';
import PedidoCard from './PedidoCard.vue';

  export default {
    name: 'Pedidos',
    components: {
      Mensagem,
      SelectStatus,
      PedidoCard,
    },

    data() {
      return {
        pedidos: [],
        statusApi:[],
        msg:'',
        statusSelecionado:""
      }
    },

    methods: {
      // Envia uma requisição GET para a api, que retorna todos o pedidos
      async getPedidos(){
        const response = await axios.get('http://localhost:3000/pedidos') 
        this.pedidos = response.data
      },
      // Envia uma requicição GET para a api, para buscar os status e renderiza-los na tela  
      async getStatus() {
        const response = await axios.get('http://localhost:3000/status')
        this.statusApi = response.data
        
        // inicializa a varialvel "statusSelecionado" com o status de "pronto"  
        this.statusSelecionado = this.statusApi[0].nome
      },

      async updatedStatus(pedido , novoStatus) {
        try {
          // Envia requisição PATCH para a API, alterando apenas o campo `status` do pedido especificado
          await axios.patch(`http://localhost:3000/pedidos/${pedido.id}`, {
            status:novoStatus
          })
          // atualiza os pedidos e status
          this.getPedidos()
          this.getStatus()

        } catch (error) {
          console.log("Erro ao atulizar o pedido" , error)
        }
      },  
       
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

        // passa a mensagem   para a variavel msg que esta sendo passado por meio de prop para o componet menssagen
        this.msg = "Pedido cancelado com sucesso!"

        // remove o alert de sucesso da tela 
        setTimeout(() => {
          this.msg = ""
        } ,1500)
      },
    },

    // // Quando o componente Pedidos for montado na tela, chama as funções getPedidos e getStatus
    mounted() {
      this.getPedidos()
      this.getStatus()
    },

    // filtra os pedidos conforme o status
    //computed monitora alteração na variavel "statusSelecionado", se houver ela faz um verificação
    computed: {
      filterStatus() {
        // Se o status selecionado for "Todos", retorna todos os pedidos
        if(this.statusSelecionado === "Todos") return this.pedidos 

         // Caso contrário, retorna apenas os pedidos com o status correspondente
        return this.pedidos.filter((p => p.status === this.statusSelecionado))
    },
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