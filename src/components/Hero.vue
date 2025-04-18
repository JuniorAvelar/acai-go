<template>
    <div class="hero-bg">
       <div class="hero-title">
        <h2>"AçaíGo: mais que um pedido, uma experiência gelada."</h2>
       </div>
       <div class="hero-img">
        <img src="/img/hero.png" alt="">
        <div class="shape"></div>
       </div>
    </div>
</template>

<script>
    export default {
        name: 'Hero'
    }
</script>


<style scoped>
    .hero-bg {
        background-color: #9E42EC;
        display: flex;
        height: 494px;

        position: relative;
    }

    .hero-img { 
        position: relative;
        flex: 1;
    }

    .hero-img img {
        width: 100%;
        z-index:2;
        position: relative;
    }

    .hero-title {
        flex: 1;
        display: flex;
        align-items: center;
        z-index: 1;
    }

    .hero-title h2 {
        font-size: 42px;
        color: #fff;
        padding: 48px;
        width: 600px;
        margin: 0 auto;
    }

    .shape {
        position: absolute;
        top:-200px;
        left:-160px;
        width: 900px;
        height: 1000px;
        background-color: #CE70A0;  
        border-top-left-radius: 50% ;
        border-bottom-left-radius: 50% ;
        z-index: 0;

    }
</style>