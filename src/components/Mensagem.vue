
<template>
    <div class="alerta-container">
        <i class="fa-solid fa-check"></i> 
        <p>Pedido enviado com sucesso!</p>                                                              
    </div>
</template>

<script>
    export default {
        name: 'Mensagem'
    }
</script>

<style scoped>
    .alerta-container {
        position: fixed;
        top: 10px;
        right: 10px;
        z-index: 99;

        width: 300px;
        height: 60px;
        background-color: #fff;
        border-radius: 8px;
        box-shadow: rgba(50, 50, 93, 0.25) 0px 6px 12px -2px, rgba(0, 0, 0, 0.3) 0px 3px 7px -3px;
        
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 5px;

    }

    .fa-solid.fa-check {
        color: green;
        font-size: 20px;
    }
</style>