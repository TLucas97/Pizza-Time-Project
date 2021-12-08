<template>
  <div class="container">
    <h1>Pedidos <img :src="check" alt="ok" id="ok"></h1>
    <Dashboard />
    <Footer />
  </div>
</template>

<script>
import Dashboard from '../components/Dashboard.vue'
import Footer from '../components/Footer.vue'

export default{
  name: 'Pedidos',
  components: {
    Dashboard,
    Footer
  },
  data(){
    return {
      check: './img/checked.png'
    }
  }
}
</script>

<style scoped>
h1{
  text-align: center;
  margin-top: 1em;
  margin-bottom: 2em;
  font-size: 3rem;
}
</style>