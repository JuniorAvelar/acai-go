<template>
    <div class="modal-orverlay">
        <div class="modal">
            <i class="fa-solid fa-trash"></i>
            <p>Deseja realmente apagar este pedido?</p>
            <div class="button-control"> 
                <button class="cancelar-button" @click="$emit('closeModal')">Cancelar</button>
                <button class="apagar-button" @click="$emit('cancelPedido')">Apagar</button>
            </div>
        </div>
    </div>
</template>


<script>
    export default {
        name: 'ModalComponent'
    }
</script>


<style scoped>
    .modal-orverlay {
        background-color: #000000db;
        left: 0;
        top: 0;
        position: fixed ;
        width: 100%;
        height: 100vh;

        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 99;
    }

    .modal {
        width: 400px;
        height: 230px;
        background-color: #fff;
        border-radius: 8px;

        display: flex;
        flex-direction: column;
        justify-content: space-between;
        padding: 20px;
    }

     .modal > p {
        text-align: center;
     }

     .button-control {
       align-self: flex-end;
     }

     .button-control > button {
        margin-left: 10px;
        height: 30px;
        width: 90px;
        border-radius: 8px;
        border: none;
        color: #fff;
        font-weight: bold;
        cursor: pointer;
     }

     .cancelar-button {
        background: #7b7b7b;
     }

     .apagar-button {
        background: red;
     }

     .fa-solid.fa-trash {
        color: rgb(249, 49, 49);
        font-size: 30px;
        text-align: center;
        /* margin-left: 20px; */
     }
</style>