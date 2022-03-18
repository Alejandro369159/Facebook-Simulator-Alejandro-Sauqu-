<template>
  <div>
     <h1>Facebook</h1>
    <label class="izquierda" for="">Ingresa el nombre del usuario </label>
    <input type="text" v-model="nombre" /> <br>
    <hr>
    <h3 style="margin:5px">Nueva Publicación</h3>
    <label for="">Escribe una descripción</label>
    <input type="text" v-model="Pdescripcion"><br>
    <label for="">Ingrese la liga de la imagen</label>
    <input type="text" v-model="Pimg">
     <br> <button class="boton" v-on:click="AgregarNueva()">Ingresar publicación</button>
  </div>

  <div v-if="Nueva!=0">
    <hr /><br />
      <b>{{ nombre }}</b>
      - {{ Pdescripcion }} <br /> <br />
     {{Pimg}}

    <div class="izquierda">
    Likes: {{ Plikes }} |
    </div>
  </div>

  <div v-for="publicacion of publicaciones">
    <hr /><br />
      <b>{{ publicacion.nombre }}</b>
      - {{ publicacion.descripcion }} <br /> <br />
      <img :src="publicacion.img" alt="" height="180" /> <br />

    <div class="izquierda">
    Likes: {{ publicacion.likes }} | <button v-on:click="DarLike(publicacion)">Dar Like</button>
    </div>
    
  </div>
</template>

<script>
const axios = require('axios');
export default {
  data() {
    return {
      publicaciones: [],
      nombre: '',
      publicacion: '',
      Pdescripcion:'',
      Pimg:'',
      Plikes:0,
      Nueva:0,
    };
  },
  methods: {
    ConsultarPublicaciones() {
      axios
        .get(
          'https://us-central1-uanl-bootcamp.cloudfunctions.net/api/publicaciones'
        )
        .then((response) => {
          this.publicaciones = response.data;
        });
    },
    DarLike(publicacion){
      if(publicacion.likes==0){
        publicacion.likes++;
      }
    },
    AgregarNueva(){
      this.Nueva=1;
    },
    PDarlike(){
      if(this.Plikes==0){
        this.Plikes++;
      }
    },
  },
  mounted() {
    this.ConsultarPublicaciones();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.centrado {
  text-align: center;
}
.izquierda {
  text-align: left;
}
.boton{
  margin-top:15px;
  padding:10px;
}
</style>
