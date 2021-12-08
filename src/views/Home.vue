<template>
  <div class="container">
    <Banner />
    <div id="formulario">
    <PizzaForm />
    <Footer />
    </div>
  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import PizzaForm from '../components/PizzaForm.vue'
import Footer from '../components/Footer.vue'

export default{
  name: 'Home',
  components: {
    Banner,
    PizzaForm,
    Footer
  }
}
</script>

<style scoped>
#formulario{
  background: rgb(245, 245, 245);
  height: 500px;
}

</style>
