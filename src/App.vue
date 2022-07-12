<template>
  <div id="app">
    <HeaderBoolfix
    @sendText="searchtext" />

     <main>
    <FilmMain :arrayFilm="this.arrayFilm" />
  </main>
  </div>
  
</template>

<script>

import HeaderBoolfix from './components/HeaderBoolfix.vue'
import FilmMain from './components/FilmMain.vue'
import axios from "axios"


export default {
  name: 'App',
  data(){
    return{
      arrayFilm: [],
      searchtext: "",
    }
  },
  components: {
    HeaderBoolfix,
    FilmMain
  },
  mounted(){
    this.searchfilm();
  },
  methods:{
    searchfilm(){
      if(this.searchtext !== ""){
        axios.get(`https://api.themoviedb.org/3/movie/550?api_key=026400b00d6e67fa4fe97ad66c83a3fe&query=${this.textToSearch}&language=it-IT`)
        .then(response =>{
          this.arrayFilm = response.data.results;
        })
      }else{
        axios.get(`https://api.themoviedb.org/3/movie/top_rated?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=it-IT&page=1`)
          .then(response => {       
          this.arrayFilm = response.data.results;
        })
      }
    },
    searchText(text){
      this.searchtext = text;
      this.searchtext = this.searchtext.replace(" ","+")
      this.searchfilm(); 
    }
  }
}
</script>

<style lang="scss">
 @import "src/style/common.scss";
   #app{
    height: 300vh;
    width: 100%;
    background-color: lightgray;
  }
</style>
