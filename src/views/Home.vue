<template>
  <div class="home">
    <v-row class="d-flex justify-center mt-5">
      <v-col cols="4">
        <v-text-field
          v-model="search"
          @keypress.enter="searchIcon()"
          outlined
          rounded
          prepend-icon="mdi-search"
        >
        </v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="3" v-for="(icon, name) in iconsPagination" :key="name">
        <IconRendererVue :name="name" :icon="icon"></IconRendererVue>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-pagination
          v-model="currentPage"
          :length="Math.ceil(iconlength / pageSize)"
        ></v-pagination>
      </v-col>
    </v-row>
  </div>
</template>
<style>
.tarjetero {
  display: flex;
  width: 100%;
  justify-content: space-between;
  background-color: cyan;
  flex-wrap: wrap;
}

.tarjeta {
  width: 30%;
  background-color: white;
  border: 1px solid #000;
}
</style>
<script>
import IconRendererVue from "../components/IconRenderer.vue";
import { icons } from "../assets/icons.js";
// @ is an alias to /src
export default {
  name: "Home",
  components: { IconRendererVue },
  data: () => ({
    title: "David dice hola",
    texto: "",
    holder: "Escribe un texto",
    tipo: "password",
    info: [],
    filteredIcons: null,
    search: "",
    currentPage: 1,
    pageSize: 50,
    icons: icons,
  }),
  computed: {
    iconlength() {
      return this.filteredIcons
        ? Object.keys(this.filteredIcons).length
        : Object.keys(this.icons).length;
    },
    iconsPagination() {
      const iconKeys = this.filteredIcons
        ? Object.keys(this.filteredIcons)
        : Object.keys(this.icons);
      const startIndex = this.currentPage * this.pageSize - this.pageSize;
      const endIndex = startIndex + this.pageSize;

      const paginatedKeys = iconKeys.slice(startIndex, endIndex);
      const paginatedIcons = {};
      console.log(paginatedKeys);
      paginatedKeys.forEach((key) => {
        if (this.filteredIcons) {
          paginatedIcons[key] = this.filteredIcons[key];
        } else {
          paginatedIcons[key] = this.icons[key];
        }
      });

      return paginatedIcons;
    },
  },
  methods: {
    cambiarTitulo(titulo) {
      this.title = titulo;
    },
    ocultarTexto() {
      if (this.tipo === "password") {
        this.tipo = "text";
      } else {
        this.tipo = "password";
      }
    },
    searchIcon() {
      const search = this.search.toLowerCase();
      const iconKeys = Object.keys(this.icons);
      const filteredIcons = {};
      iconKeys.forEach((key) => {
        if (key.includes(search)) {
          filteredIcons[key] = this.icons[key];
        }
      });

      this.filteredIcons = filteredIcons;
    },
  },
  created() {
    fetch("http://smgpuntosdeventa.net/palabras/")
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        this.info = data.palabras;
      });
  },
};
</script>
