<template>
  <Navbar :logo="logo_src" :alt="app_name"/>
  <router-view/>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'

export default{
  components: {
    Navbar,
    Footer
  },
  data(){
    return{
      logo_src: './img/pizza-logo.png',
      app_name: 'pizza-time'
    }

  }
}

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;500&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@700&family=Roboto:wght@100;300;500&display=swap');
*{
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  scroll-behavior: smooth;
}



#heart{
  color: red;
  font-size: 3.5rem;
}
</style>