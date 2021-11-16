<template>
 <div class="text-center mt-5 mb-4">
     <div class="input-group mx-auto" style="max-width:500px">

         <select
         class="form-control fs-3" 
         placeholder="Type the genre..."

         v-model="searchGenre"

        @keydown.enter="startSearch">

        <option value="">All Genre</option>
        <option value="rock">Rock</option>
        <option value="pop">Pop</option>
        <option value="jazz">Jazz</option>
        <option value="metal">Metal</option>

        </select>

        <button class="btn btn-outline-primary" type="button"

        @click="startSearch"
        >SEARCH</button>

     </div>

     <p class="mt-3 mb-4 text-white fs-3">Show Genre: 
         <strong class="mx-3 fs-2">{{searchGenre}}</strong>
         <button class="btn-close btn-close-white btn-close-fs-1" @click="resetLista"></button></p>


 </div>

    
</template>

<script>
export default {
    name: "searchbar",
    data(){
        return{
            searchGenre:"",
        };
    },
    methods:{
        startSearch(){
            this.$emit("startSearch",this.searchGenre);
        },
        resetLista(){
          this.searchGenre="" ;
          this.$emit("allAlbum");
        }
    }
    }
</script>