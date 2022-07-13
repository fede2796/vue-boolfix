<template>
  <!-- Cards Container -->
  <div class="container-fluid">
    <!-- Section Name -->
    <div class="sectionTitle">Film</div>
    <!-- Horizontal Scroller -->
    <div class="row row-cols-5 py-1 horizonal-scroll">     
      <div class="col" v-for="film in filmArray" :key="film.id">
        <FilmComponent :Film="film" :GenreSerieArray="GenreSerieArray"/>
      </div>
    </div>
    <!-- Section Name -->
    <div class="sectionTitle">Serie TV</div>
    <!-- Horizontal Scroller -->
    <div class="row row-cols-5 py-1 horizonal-scroll">
      <div class="col" 
      v-for="serie in serieArray" 
      :key="serie.id">
        <SerieComponent :Serie="serie" :textToSearch="textToSearch"/>
      </div>
    </div>
  </div>
</template>

<script>
  // Import
  import SerieComponent from './SerieComponent.vue';
  import FilmComponent from './FilmComponent.vue';
  
  export default {
    name: "BoolflixComponent",
    components: {
      FilmComponent,
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
  // section Style
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