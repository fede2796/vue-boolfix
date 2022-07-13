<template>
  <div class="container-fluid">
    <div class="sectionTitle">Film</div>
    <div class="row row-cols-4 py-1 horizonal-scroll">
      <div class="col" v-for="film in filmArray" :key="film.id">
        <ComponentFilm :Film="film" :GenreSerieArray="GenreSerieArray"/>
      </div>
      <div class="sectionTitle">Serie TV</div>
       <div class="row row-cols-4 py-1 horizonal-scroll"> 
        <div class="col" v-for="serie in serieArray" :key="serie.id">
        <SerieComponent :Film="serie" :textToSearch="textToSearch"/>
      </div></div>
     
    </div>
  </div>
</template>

<script>
  import ComponentFilm from './ComponentFilm.vue';
  import SerieComponent from './SerieComponent.vue';
  export default {
    name: "BoolflixComponent",
    components: {
      ComponentFilm,
      SerieComponent,
    },
    props:{
      filmArray: Array,
      serieArray: Array,
      textToSearch: String,
      GenreFilmArray: Array,
      GenreSerieArray: Array,
    }
  }
</script>

<style lang="scss" scoped>
   .container-fluid{
    padding-bottom: 80px;
    height: 100%;
    .sectionTitle{
      font-size: 30px;
      margin: 10px 15px;
      font-weight: 600;
    }
    // setting horizontal scrolling
    .horizonal-scroll{
      height: calc(60% - 40px);
      flex-wrap: nowrap;
      overflow-x: auto;
      overflow-y: hidden;
      flex-shrink: 0;
      
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
  }
</style>