<template>
  <div class="bg-color">
    <div class="container">
    <!--Aggiungo barra di ricerca-->
    <SearchBar
    @startSearch="albumFilter"
    @allAlbum="showAlbum"
    ></SearchBar>

      <div class="row row-cols-5">
        <div class="col mb-3" v-for="(album, i) in filterList" :key="i">
          <AlbumCard
            :title="album.title"
            :author="album.author"
            :poster="album.poster"
            :year="album.year"
            :genre="album.genre"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AlbumCard from "./AlbumCard.vue";
import axios from "axios";
import SearchBar from "./SearchBar.vue"

export default {
  name: "AlbumContainer",
  components: {
    AlbumCard,
    SearchBar,
  },
  data() {
    return {
      arrayAlbum: [],
      searchGenre: "",
    };
  },
  //Aggiunto methods per filtrare e il computed per creare la variabile della ricerca una sola volta
   methods: {
    albumFilter(genre) {
      this.searchGenre = genre;
      console.log("searchGenre is " + this.searchGenre);
    },
    showAlbum() {
        this.searchGenre ="";
    }
  },
  computed: {
    filterList() {
      if (!this.searchGenre) {
        return this.arrayAlbum;
      }
      return this.arrayAlbum.filter(el => {
        return el.genre.toLowerCase().includes(this.searchGenre.toLowerCase().trim())
      });
    
      
    },
  },

  mounted() {
    axios.get("https://flynn.boolean.careers/exercises/api/array/music")
    .then((resp) => {
        this.arrayAlbum = resp.data.response;
      });
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
.bg-color {
  background-color: #192d3b;
  padding: 25px;
}
</style>