<template>
   <div class="nav-container">
    <div class="logo">
        
        <h1>AcaíGO</h1>
    </div>
        <nav>
            <router-link to="/">Home</router-link> 
            <router-link to="/Pedidos">Pedidos</router-link>
        </nav>
   </div>
</template>


<script>
    export default {
        name:'NavBar'
    }
</script>

<style scoped>
    .nav-container{
        display: flex;
        justify-content: space-between;
        align-items: center;

        padding: 10px 40px;
        background-color: #9E42EC;
        color:#fff;

    }

    nav a{
        list-style: none;
        text-decoration: none;
        margin: 12px;
        color:#fff;
        font-weight: bold;
        transition: 0.4s;
        z-index: 10;
        position: relative;
    }

    nav a:hover {
        opacity: 0.8;
    }
</style>