<template>
  <div class="home">
    <h1>
      {{title}}
    </h1>
    <input :type="tipo" v-model="texto" :placeholder="holder"/>
    <button @click="ocultarTexto()">Ocultar</button>
    <button @click="cambiarTitulo(texto)">Cambia el titulo</button>
    <div class="tarjetero">
      <!--Aqui empezo la tarjeta nueva-->
      <v-card
        class="mx-auto tarjeta my-2"
        color="#26c6da"
        theme="dark"
        max-width="400"
        prepend-icon="mdi-twitter"
        title="Twitter"
        v-for="(item, key) in info" :key="key"
      >
        <v-icon size="x-large">mdi-Pokeball</v-icon>

        <v-card-text class="text-h5 py-2">
          {{item.english}}
        </v-card-text>
        <v-card-text class="text-h5 py-2">
          {{item.spanish}}
        </v-card-text>
      </v-card>
    </div>
  </div>
</template>
<style>
.tarjetero{
  display: flex;
  width: 100%;
  justify-content: space-between;
  background-color: cyan;
  flex-wrap: wrap;
}
.tarjeta{
  width: 30%;
  background-color: white;
  border: 1px solid #000;
}
</style>
<script>
// @ is an alias to /src
export default {
  name: 'Home',
  components: {

  },
  data: () => ({
    title: "Junue es adorable",
    texto: "",
    holder: "Escribe un texto",
    tipo: "password",
    info: []
  }),
  methods: {
    cambiarTitulo(titulo){
      this.title =  titulo
    },
    ocultarTexto(){
      if(this.tipo === "password") {
        this.tipo = "text"
      } else {
        this.tipo = "password"
      }
    }
  },
  created(){
    fetch("http://smgpuntosdeventa.net/palabras/")
    .then(response => response.json())
    .then(data => {
      console.log(data)
      this.info = data.palabras
    })
  }

}
</script>
