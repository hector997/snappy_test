<template>
  <div class="container" id="app">
    <nav class="level mb-0">
      <div class="navbar-brand">
        <img id="logo" class="image is-32x32" alt="snappy logo" src="./assets/logo.svg">
        <h1 class="title">Snappy Labs</h1>
        </div>
    </nav>
    <container v-on:sent="team2" />
  </div>
</template>

<script>
import Container from './components/container.vue'

export default {
  name: 'App',
  
  components: {
    Container,
  },
   data() {
    return {
      team2:'',
      }
    },
    methods: {
 
        addTeam(team2){
          console.log('recieved:  ')
          console.log(team2);
          //this.team = [...this.team, newTeam];
        }
      },
}
</script>

<style>
@import "~bulma/css/bulma.css";


#app {
  font-family: Poppins,sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 30px;
}

</style>
