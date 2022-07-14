<template>
  <div id="app">
    <!-- Header Component -->
    <HeaderComponent 
    @sendText="searchText"
    @sendValue="genreValue"
    :GenreFilmArray="this.GenreFilmArray"
    :GenreSerieArray="this.GenreSerieArray"
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
import HeaderComponent from './components/headerComponent.vue';
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
      Genre: "",
    }
  },
  components: {
    HeaderComponent,
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
        axios.get(`https://api.themoviedb.org/3/search/movie?language=en-US&with_genres=${this.Genre}&api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&query=${this.textToSearch}`)
        .then(response => {
          this.Genre = "All";         
          this.filmArray = response.data.results.splice(0,14);
          this.textToSearch = "";
        })
      } else if(this.Genre === "All"){
        axios.get(`https://api.themoviedb.org/3/discover/movie?language=en-US&api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&with_genres=${this.Genre}`)
        .then(response => {        
          this.filmArray = response.data.results.splice(0,14);
          
        })
      } else if(this.Genre !== "" || this.Genre !== "All"){
        axios.get(`https://api.themoviedb.org/3/discover/movie?language=en-US&api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&with_genres=${this.Genre}`)
        .then(response => {        
          this.filmArray = response.data.results.splice(0,14);
        })
      } else {
        // altrimento stampo i risultati della ricarca
        axios.get(`https://api.themoviedb.org/3/movie/top_rated?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=it-IT&page=1`)
        .then(response => {      
          this.filmArray = response.data.results.splice(0,14);
        })
      }     
    },
    searchAllTvSeries(){
       // PER LE SERIE TV controllo se è la stringa è vuota cosi printo una pagina inziale
      if(this.textToSearch !== ""){
        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&query=${this.textToSearch}&language=it-IT`)
        .then(response => { 
          this.Genre = "All";       
          this.serieArray = response.data.results.splice(0,14);
          this.textToSearch = "";
        })
      } else if(this.Genre === "All"){
        axios.get(`https://api.themoviedb.org/3/discover/tv?language=en-US&api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&with_genres=${this.Genre}`)
        .then(response => {        
          this.serieArray = response.data.results.splice(0,14);
          
        })
      } else if(this.Genre !== "" || this.Genre !== "All"){
        axios.get(`https://api.themoviedb.org/3/discover/tv?language=en-US&api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&with_genres=${this.Genre}`)
        .then(response => {        
          this.serieArray = response.data.results.splice(0,14);
          
        })
      } else {
        // altrimento stampo i risultati della ricarca
        axios.get(`https://api.themoviedb.org/3/tv/top_rated?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=it-IT&page=1`)
        .then(response => {       
          this.serieArray = response.data.results.splice(0,14);
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
    },
    genreValue(genre){
      // prendo il testo della ricerca e lo salvo in una variabile
      this.Genre = genre;
      console.log(this.Genre);
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
  }
</style>