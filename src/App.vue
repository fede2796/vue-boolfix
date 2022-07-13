<template>
  <div id="app">
    <!-- Header Component -->
    <headerComponent 
    @sendText="searchText"
    />

    <!-- Main -->
    <main>

      <!-- Compent principale del main per stampare a cui passo tutti i dati -->
      <BoolflixComponent 
      :filmArray="this.filmArray" 
      :serieArray="this.serieArray"
      :GenreFilmArray="this.GenreFilmArray"
      :GenreSerieArray="this.GenreSerieArray"
      :textToSearch="this.textToSearch"/>
    </main>

  </div>
</template>

<script>
// IMPORT
import headerComponent from './components/headerComponent.vue';
import BoolflixComponent from './components/BoolflixMainComponent.vue';
import axios from "axios";
export default {
  name: 'App',
  data(){
    return{
      filmArray: [],
      serieArray: [],
      GenreFilmArray: [],
      GenreSerieArray: [],
      textToSearch: "",
    }
  },
  components: {
    headerComponent,
    BoolflixComponent,
  },
  mounted(){
    // funzini che devono partite all'inizio
    this.searchAllFilms();
    this.searchAllTvSeries();
    this.searchAllMovieGenre();
    this.searchAllTvGenre();
  },
  methods: {   
    // Faccio le chiamate axios che mi servono 
    searchAllFilms(){
      // PER I FILM controllo se è la stringa è vuota cosi printo una pagina inziale
      if(this.textToSearch !== ""){
        axios.get(`https://api.themoviedb.org/3/search/movie?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&query=${this.textToSearch}&language=it-IT`)
        .then(response => {        
          this.filmArray = response.data.results.splice(0,10);
        })
      } else {
        // altrimento stampo i risultati della ricarca
        axios.get(`https://api.themoviedb.org/3/movie/top_rated?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=it-IT&page=1`)
        .then(response => {      
          this.filmArray = response.data.results.splice(0,10);
        })
      }     
    },
    searchAllTvSeries(){
       // PER LE SERIE TV controllo se è la stringa è vuota cosi printo una pagina inziale
      if(this.textToSearch !== ""){
        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&query=${this.textToSearch}&language=it-IT`)
        .then(response => {        
          this.serieArray = response.data.results.splice(0,10);
        })
      } else {
        // altrimento stampo i risultati della ricarca
        axios.get(`https://api.themoviedb.org/3/tv/top_rated?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=it-IT&page=1`)
        .then(response => {       
          this.serieArray = response.data.results.splice(0,10);
        })
      }     
    },
    searchAllMovieGenre(){ 
      // Scarico l' arrey dei generi dei film
      axios.get(`https://api.themoviedb.org/3/genre/movie/list?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60`)
      .then(response => {        
        this.GenreFilmArray = response.data.genres;
      }) 
    },
    searchAllTvGenre(){
      // Scarico l' arrey dei generi delle serie tv
      axios.get(`https://api.themoviedb.org/3/genre/tv/list?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60`)
      .then(response => {        
        this.GenreSerieArray = response.data.genres;
      })  
    },
    searchText(text){
      // prendo il testo della ricerca e lo salvo in una variabile
      this.textToSearch = text;
      // cambio gli spazzi con il simbolo +
      this.textToSearch = this.textToSearch.replace(" ","+")
      // richiamo le funzioni per cercare il film
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
    background-color: #222;
    min-height: 100vh;
    // Scrollbar Modification
      &::-webkit-scrollbar {
        width: 10px;
        height: 22px;
      }
      &::-webkit-scrollbar-thumb:hover {
        background-color: grey;
      }
      &::-webkit-scrollbar-thumb {
        background-color: #222;
        border-radius: 20px;
        border: 6px solid transparent;
        background-clip: content-box;
      }
  }
</style>