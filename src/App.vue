<template>
 <div>
  <NavBar/>
  <router-view/>
  <Footer/>
 </div>

</template>

<script>
  import NavBar from './components/NavBar.vue';
  import Footer from './components/Footer.vue';
  export default {
    components: {
      NavBar,
      Footer,
    }
  }
</script>

<style>

  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: helvetica;
  }
</style>
