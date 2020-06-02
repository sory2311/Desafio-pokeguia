<template>
  <div id="app">
<img class="la" src="https://i2.wp.com/www.cargando.net/wp-content/uploads/2012/12/pokemon-logo.gif?resize=618%2C456" alt="">
     <h1>PokeGuía</h1>
     <label for="text">Nombre</label>
    <input type="text" v-model="name">
   <button @click="buscarPokemon">Buscar Pokémon</button> 
   <h2>{{getNombre}}</h2>
   <img :src="getImagen" alt />

  <div class="container d-flex flex-column justify-content-start align-items-center">
  <div class="row">
    <div class="col-6">
      <h2 class="hab">Habilidades</h2>
   <ol>
     <li v-for="(habilidad,index) in getHabilidades" :key="index">{{habilidad.ability.name}}</li>
   </ol>
    </div>
    <div class="col-6">
      <h2 class="mov">Movimientos</h2>
   <ol>
     <li v-for="(move,index) in getMovimiento" :key="index">{{move.move.name}}</li>
   </ol>
    </div>
  </div>
  </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      name:"",
     datos: {},
     picture: ""
    };
  },
  methods: {
    buscarPokemon(){
      fetch("https://pokeapi.co/api/v2/pokemon/" + this.name)
      .then(res => res.json())
      .then(data => {
        this.datos = data;
      });
    }
    },
    created(){
      fetch("https://pokeapi.co/api/v2/pokemon/pikachu" )
      .then(res => res.json())
      .then(data => {
        this.datos = data;
      });
    },
    computed:{
      getNombre(){
        return this.datos.name;
      },
      getImagen(){
        if (this.datos.sprites){
          return this.datos.sprites.front_default
        }else{
          return "";
        }
      },
      getHabilidades(){
        return this.datos.abilities.slice(0, 15);
      },
       getMovimiento(){
        return this.datos.moves.slice(0, 15);
      }     
    }
  };

</script>

<style>
body{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #091b2e;
  text-align: center;
  margin: 20px;
}

.la{
  width: 25%;
}


h1, .hab, .mov{
  color: rgb(15, 15, 117);
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}
 button, label{
  font-weight: bold;
 }
 
</style>


