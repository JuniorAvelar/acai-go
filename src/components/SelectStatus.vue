<template>
    <div>
      <select class="select-status" @change="$emit('update:statusSelecionado' , $event.target.value)">
      <option  v-for="status in statusApi" :key="status.id" :value="status.nome">{{ status.nome }}</option>
    </select>
    </div>
</template>

<script>
    export default {
        name:'SelectStatus',

        data() {
            return {
            }
        },
        props:{
            statusApi: {
                type:Array,
                required:true
            },

            statusSelecionado: {
                type:String,
                required:true
            }
        },
    }
</script>

<style scoped >
    .select-status {
        padding: 5px;
        font-size: 14px;    
        border-radius: 8px;
        width: 150px;
        border: none;
        background: #D9D9D9;
        margin-left: 40px;
  }
</style>