<template>
  <div class="home">
    <Hero/>
    <Form/>
  </div>
</template>

<script>
import Hero from '@/components/Hero.vue';
import Form from '@/components/Form.vue';
export default {
  name: 'HomeView',
  components: {
    Hero,
    Form,
  }
}
</script>
