<template>
    <Mensagem v-show="msg" :msg="msg"/>
    <div class="form-container">
            <h2>Monte seu pedido</h2>
        <form @submit="getPedidos($event)"  id="form" >
            <div class="input-control">
                <label for="">Nome do cliente:</label>
                <input type="text" placeholder="Digite seu nome" v-model="nome" required>
            </div>

            <div class="buttons-tamanho">
                <label >Tamanho:</label>
                <div class="buttons-control">
                    <button v-for="t in tamanhoApi" :key="t.id" @click="tamanho = t.nome" :class="{ active: tamanho === t.nome}">{{ t.nome }}</button>
                </div>
            </div>

            <div class="base-container">
                <label for="">Escolha a base:</label>
                <select v-model="baseSelecionada">
                    <option value="">Selecione a base</option>
                    <option v-for="base in basesApi" :key="base.id" :value="base.nome">{{ base.nome }}</option>
                </select>
            </div>

            <div class="Ingredientes-container" >
                <label>Escolha os Ingredientes:</label> 
                <h4>Frutas:</h4>
                <div class="checkbox-control">
                   <div class="checkbox-container" v-for="fruta in frutasApi" :key="fruta.id" >
                    <input type="checkbox" :value="fruta.nome" v-model="frutasSelecionadas"> 
                    <label for="">{{ fruta.nome }}</label>
                   </div>
                </div>

                <h4>Cremes:</h4>
                <div class="checkbox-control">
                   <div class="checkbox-container" v-for="creme in cremesApi" :key="creme.id">
                    <input type="checkbox" :value="creme.nome" v-model="cremesSelecionados" > 
                    <label for="">{{ creme.nome }}</label>
                   </div>
                </div>
            </div>

            <div class="obs-container">
                <label for="">Observações:</label>
                <textarea v-model="observacao" placeholder="Deixe aqui alguma observação..."></textarea >
            </div>
            
          <div class="button-control">
            <button class="comfimar-button" value="submit">Confirmar Pedido</button>
          </div>
        </form>
    </div>
</template>

<script>
import axios from 'axios';
import Mensagem from './Mensagem.vue';
    export default {
        name: 'Form',

        components: {
            Mensagem,
        },

        data() {
          return {
            nome: '',
            tamanho: '',
            baseSelecionada: '',
            frutasSelecionadas: [],
            cremesSelecionados: [],
            observacao: [],

            frutasApi: [],
            cremesApi: [],
            basesApi: [],
            tamanhoApi: [],

            msg: ""
          }
        },

      methods: {
        getPedidos(e) {
            e.preventDefault()
            const pedido = {
                nome: this.nome,
                tamanho: this.tamanho,
                base: this.baseSelecionada,
                frutas: this.frutasSelecionadas,
                cremes: this.cremesSelecionados,
                observacao: this.observacao,
                status: 'Solicitado',
            }

            try {
                const response = axios.post('http://localhost:3000/pedidos' , pedido)
                console.log(response.data)
            } catch (error) {
                console.log('erro ao enviar pedido:' , error)
            }

            this.nome = ""
            this.tamanho = ""
            this.baseSelecionada = ""
            this.frutasSelecionadas = []
            this.cremesSelecionados = []
            this.observacao = ""

            this.msg = "Pedido enviado com sucesso!"

            setTimeout(() => {
                this.msg = false
            }, 2000)

        },

        async getIgredientes() {
            try {
                const response = await axios.get('http://localhost:3000/ingredientes')
                this.frutasApi = response.data.frutas
                this.cremesApi = response.data.cremes
            }catch(error) {
                console.log(error)
            }
        },

        async getBase() {
           try {
            const response = await axios.get('http://localhost:3000/bases')
            this.basesApi = response.data
           } catch (error) {
            console.log(error)
           }
        },

        async getTamanho() {
            try {
                const response = await axios.get('http://localhost:3000/tamanhos') 
                this.tamanhoApi = response.data
            } catch (error) {
                console.log(error)
            }
        }
      },

      mounted() {
        this.getIgredientes()
        this.getBase()
        this.getTamanho()
      }
    }
</script>

<style scoped>

    .form-container {
        position: relative;
        z-index: 1;
        height: auto;
        background-color: #fff;
    }

    .form-container label {
        font-size: 20px;
        font-weight: 300;
        margin-bottom: 1rem;
        margin-top:1rem ;
    }

    .form-container h2 {
        position: relative;
        text-align: center;
        font-size: 40px;
        padding: 3rem 0;
        color: #200D2F;
    }

    .form-container h2::after {
        content: '';
        position: absolute;
        bottom: 40px;
        left: 40%;
        height: 7px;
        width: 300px;
        border-radius: 20px;
        background: #CE70A0;
    }

    #form {
        max-width: 600px;
        margin: 0 auto;
    }

    .input-control {
        display: flex;
        flex-direction: column;
    }

    .input-control input {
        padding: 10px;
        font-size: 14px;
        border-radius: 8px;
        border: none;
        background: #D9D9D9;

    }

    .input-control input::placeholder {
        color: #1b1a1a;
        font-weight: 400;
    }

    .buttons-tamanho{
        display: flex;
        flex-direction: column;
    }

    .buttons-control button {
        border-radius: 20px;
        width: 100px;
        height: 45px;
        padding: 10px;
        border: solid 1px #ccc;
        cursor: pointer;
        transition: 0.4s;
        background-color: #D9D9D9;
    }

    .buttons-control button:hover {
        background: #b4b4b4;
    }

    .buttons-control {
        display: flex;
        gap: 12px;
    }

    .active {
     outline: solid 4px rgb(59, 140, 215);
        }

    .base-container {
        display: flex;
        flex-direction: column;
    }

    .base-container select {
        padding: 10px;
        font-size: 14px;
        border-radius: 8px;
        border: none;
        background: #D9D9D9;
    }

    .Ingredientes-container {
        display: flex;
        flex-direction: column ;
    }

    .Ingredientes-container .checkbox-control {
      display: flex;
      flex-wrap: wrap;
    }

    .checkbox-container {
       width: 50%;
       display: flex;
       align-items: center;
       gap: 10px;
    }   

    .checkbox-control label {
        font-size: 16px;
    }

       /* checkbox */

    .checkbox-container input {
        width: 20px;
        height: 20px;
        cursor: pointer;
        border: none;
    	}

    .obs-container {
        display: flex;
        flex-direction:column;
        resize: none;
    }

    .obs-container  label {
        font-size: 20px;
        font-weight: 300;
        margin: 1rem 0;
    }

    .obs-container textarea {
        resize: none;
        height: 200px;
        border-radius: 8px;
        border: solid 1px #ccc;
        background-color: #d3d3d3;
        padding: 20px;
    }

    .obs-container textarea::placeholder {
        color: #1b1a1a;
    }

    .button-control .comfimar-button {
        color: #fff;
        background-color: #6C1DAB;
        border:none;
        width: 300px;
        height: 50px;
        font-weight: bold;
        font-size: 18px;
        border-radius: 8px;
        cursor: pointer;
        margin: 3rem 0;
        transition: linear 0.4s;
    }

    .button-control .comfimar-button:hover {
        color: #6C1DAB;
        background-color: #fff;
        border: solid 1px #6C1DAB;
    }

    .button-control {
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>

