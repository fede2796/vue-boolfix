<template>
  <!-- Card -->
  <div class="film">
    <!-- Card Image -->
    <img class="film_poster" :src="getImg(Film.poster_path)" :alt="Film.title">
    <div class="wrapper">
      <div class="genre-side" v-for="(singlefilm,index) in Film.genre_ids" :key="index">{{ getGenre(singlefilm) }}</div>
    </div>
    
    <!-- Hover effect on the card -->
    <div class="hoverEffect">
      <div>
        <span>Titolo: </span>{{ Film.title ? Film.title : Film.name }}
      </div>
      <div>
        <span>Titolo originale: </span>{{ Film.original_title ? Film.original_title : Film.original_name }}
      </div>
      <div>
        <span>Cast: </span><span class="cast">{{ this.namesCast }}</span>
      </div>
      <div>
        <img class="flags" :src="getFlags(Film.original_language)" alt="dd">
      </div>
      <div>
        <span>voto: </span>
        <!-- creo 5 stelline e le coloro in base al risultato della function -->
        <span><i class="fa-solid fa-star star-space" :class="{'star': n <= getStars(Film.vote_average)}" v-for="n in 5" :key="n"></i></span>
      </div>
      <!-- controllo se il film non abbia descrizione -->
      <div v-if="Film.overview !== '' ">
        <span>overview: </span>
        <div class="scroll">
          <span class="overview-text">{{ Film.overview }}</span>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "FilmComponent",
  props:{
    Film:Object,
    GenreFilmArray: Array,
  },
  data(){
    return{
      castArray: [],
      namesCast: "",
    }
  },
  mounted(){
    this.getCast(this.Film);
  },
  methods:{  
    //vedo quali flags non vengono rilevate e le sostituisco 
    getFlags(nazionalita){
      
      if(nazionalita == 'en'){
        nazionalita = "gb";
      } else if(nazionalita == 'ja'){
        nazionalita = "jp";
      } else if(nazionalita == 'hi'){
        nazionalita = "in";
      } else if(nazionalita == 'cs'){
        nazionalita = "cz";
      } else if(nazionalita == 'ko'){
        nazionalita = "kr";
      } else if(nazionalita == 'sv'){
        nazionalita = "ch";
      } else if(nazionalita == 'fa'){
        nazionalita = "af";
      }
      // poi ritorno la bandiera
      return `https://countryflagsapi.com/png/${nazionalita}`;
    },
    getImg(path){
      // controllo se l'img sia diversa da null
      if(path === null){
        // se è uguale allora gli do una di default
        return 'https://adriaticaindustriale.it/wp-content/uploads/2020/02/not-found.png'
      }
      // altrimenti la faccio stampare
      return `https://image.tmdb.org/t/p/w342${path}`
    },
    getStars(star){    
      // divido star che è un valore di 1 a 10 / 2
      const starcount = Math.round(star)
      // poi lo arrotondo per eccesso
      return starcount / 2;
    },
     getCast(textToSearch){  
      const search = textToSearch.id;
      // faccio una chiamata axios con search che varra come l'id del film
      axios.get(`https://api.themoviedb.org/3/movie/${search}/credits?api_key=5815a78aa9854a6ec9c6ecbc2b07ad60&language=en-US`)
      .then(response => {
        // assegno stringa vuota a namesCast 
        this.namesCast = "";
        // se il cast è maggiore di 5 stampo solo i primi 5
        if(response.data.cast.length > 5){
          for (let i = 0; i < 5; i++) {
            this.namesCast += response.data.cast[i].name + ", ";      
          } 
          // altrimenti se il cast = 0 dico che non ci sta il cast
        } else if(response.data.cast.length === 0) {                  
          this.namesCast = "no cast";
          // altrimenti stampo tutto il cast
        } else {
          for (let i = 0; i < response.data.cast.length; i++) {
            this.namesCast += response.data.cast[i].name + ", ";      
          } 
        }
        //se la chiamata non va buon fine scrivo no cast e cancello la console 
      }).catch(() => {
        
        this.namesCast = "no cast found";
      })    
      return this.namesCast;         
    },
    getGenre(Film){ 
      
      let genre = 0;
      for (let index = 0; index < this.GenreFilmArray.length; index++) {
        if(this.GenreFilmArray[index].id === Film){
          genre = this.GenreFilmArray[index].name;
        }    
      }
      
      return genre;
    }
  }
}
</script>
 
<style lang="scss" scoped>
  .film{   
    height: 600px;
    width: 400px;
    overflow: hidden;
    /* margin: 0 5px; */
    cursor: pointer;
    position: relative;
    .hoverEffect{
      position: absolute;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      opacity: 0;
      padding: 5px 10px;
      
      div{
        text-transform: uppercase;
        padding: 8px 0 5px;
        span{
          font-weight: 800;
          &.cast{
            font-weight: 100;
            text-transform: capitalize;
            font-size: 16px;
          }
        }
      
        .scroll{
          height: 200px;
          width: 100%;  
          overflow-y: auto;
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
          }
          .overview-text{
            font-weight: 100;
            text-transform: lowercase;
            font-size: 16px;
          }
        }       
      }
      .star-space{
        padding: 0 2px;
      }
      
      .star{
        color:yellow;       
      }
      .flags{
        width: 30px;
        height: 20px;
        display: inline;
        margin: 0 5px;
      } 
    }
    .wrapper{
      position: absolute;
      display: flex;
      flex-wrap: wrap;
      justify-content: flex-end;
      color: black;
      z-index: 50;
      bottom: 0px;    
      right: -5px;
      text-align: center;
      line-height: 20px;
      width: 100%;
      margin-bottom: 5px;
      .genre-side{
        margin: 2px 2px;
        padding: 5px;
        background-color: white;
        box-shadow: 5px 10px 8px #666;
      }
    }
    &:hover .wrapper{
      opacity: 0;
    }
    &:hover .hoverEffect{
      opacity: 1;
      background-color: rgba($color: #000000, $alpha: 0.9);
    }
    
    .film_poster{
      width: 100%;
      height: 100%;
    }
  }
</style>