<template>
    <h1>Pedidos</h1>
    <select>
      <option value="">prontos</option>
    </select>
    <div class="pedidos-container">
      <div class="pedido">
        <div class="peddido-header">
          <span>ID:</span>
          <span>Nome:</span>
        </div>
        <div class="pedido-content">
          <span>Tamaho:</span>
          <span>Base:</span>
          <span>Frutas</span>
          <span>Cremes</span>
        </div>
      </div>
    </div>

</template>

<script>
  export default {
    name: 'Pedidos',
    data() {

    }
  }
</script>

<style scoped>
   h1{
    color: #200D2F;
    font-size: 4rem;
  }
</style>