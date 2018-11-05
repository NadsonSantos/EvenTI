<template>
  <div id="app">
    <Menu></Menu>
    <Evento></Evento>
    <Credito></Credito>
    <Sobre></Sobre>
    <Sugestoes></Sugestoes>
    <Footer></Footer>
    <Media></Media>
  </div>
</template>

<script>
import Menu from './components/Menu.vue';
import Evento from './components/Evento.vue';
import Credito from './components/Credito.vue';
import Sugestoes from './components/Sugestoes.vue';
import Sobre from './components/Sobre.vue';
import Footer from './components/Footer.vue';
import Media from './components/Media.vue'
export default {
  name: 'app',
  components: {
    Menu,
    Evento,
    Credito,
    Sobre,
    Sugestoes,
    Footer,
    Media,
    
  },
  methods:{

  }
}
</script>

<style>
*{
    margin: 0%;
    padding: 0%;
    border: 0px;
    font-family: 'Poppins', sans-serif;
};

/* #app {
} */
</style>
