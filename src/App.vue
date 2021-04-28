<template>
  <div class="container" id="app">
    <nav class="level mb-0">
      <div class="navbar-brand">
        <img id="logo" class="image is-32x32" alt="snappy logo" src="./assets/logo.svg">
        <h1 class="title">Snappy Labs</h1>
        </div>
    </nav>
    <container @submit="addTeam(test)" /> <!-- esto deberia recibir lo del emit pero no -->
  </div>
</template>
<script>
import Container from './components/container.vue'

export default {
  name: 'App',
  
  components: {
    Container,
  },
   data(){
    return {
      team2:'',
      }
    },
    methods: {
        // con esta funcion deberia agarrar los datos que emitio el submit y meterlos en el json para que despues
        // el child los meta en una fila nueva
        addTeam:function(test){
          console.log('recieved:  ')
          console.log(test)
          
          //this.team = [...this.team, newTeam];
        },
        //esta funcion sobreescribe el 'nombre' del objeto. el lapicito llama a una funcion que le pasa los datos a esta. 
        //Primero tengo que hacer andar el emit
        editTeam(){

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
