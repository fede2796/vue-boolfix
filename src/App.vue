<template>
  <div id="app">
    <HeaderBoolfix
    @sendText="searchText"
    />

    <main>
      <FilmMain :filmArray="this.filmArray" :serieArray="this.serieArray"/>
    </main>

  </div>
</template>

<script>
import HeaderBoolfix from './components/HeaderBoolfix.vue'
import axios from "axios"
import FilmMain from './components/FilmMain.vue'
export default {
  name: 'App',
  data(){
    return{
      filmArray: [],
      serieArray: [],
      textToSearch: "",
    }
  },
  components: {
    HeaderBoolfix,
    FilmMain
},
  mounted(){
    this.searchAllFilms();
    this.searchAllTvSeries();
  },
  methods: {    
    searchAllFilms(){
      
      if(this.textToSearch !== ""){
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&query=${this.textToSearch}&language=it-IT`)
        .then(response => {        
          this.filmArray = response.data.results;
        })
      } else {
        axios.get(`https://api.themoviedb.org/3/movie/top_rated?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=it-IT&page=1`)
        .then(response => {       
          this.filmArray = response.data.results;
        })
      }     
    },
    searchAllTvSeries(){
      
      if(this.textToSearch !== ""){
        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&query=${this.textToSearch}&language=it-IT`)
        .then(response => {        
          this.serieArray = response.data.results;
        })
      } else {
        axios.get(`https://api.themoviedb.org/3/tv/top_rated?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=it-IT&page=1`)
        .then(response => {       
          this.serieArray = response.data.results;
        })
      }     
    },
    searchText(text){
      this.textToSearch = text;
      this.textToSearch = this.textToSearch.replace(" ","+")
      this.searchAllFilms(); 
      this.searchAllTvSeries();
    }
  }
}
</script>

<style lang="scss">
  @import "src/style/common.scss";
  #app{
    width: 100%;
    background-color: grey;
  }
</style>