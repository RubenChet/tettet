<template>
  <div>
    <Nav></Nav>
    <component :is="currentView" :WhichDomaine="User_Domaine"></component>
    <Not></Not>
  </div>
</template>

<script>
import Home from './components/Home.vue';
import Main from './components/Not.vue'
import Nav from './components/Navbar.vue'
import Not from './components/Not.vue';

export default {
  data: () => ({
    currentView: Home,
    User_Domaine: ""
  }),
  mounted() {
    this.$root.$on("Home.ChangePage", msg => {
      this.currentView = Main
      this.User_Domaine = msg
    })
  },
  components: {
    Home,
    Main,
    Nav,
    Not
  },
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap');
html{
  background-color: #1A3B29;
  font-family: 'Roboto Mono', monospace;
}
body{
  margin: 0!important;
}
.vs-navbar-content{
  position: relative!important;
}

</style>