<template>
  <!-- Cards Container -->
  <div class="container-fluid">
    <!-- Section Name -->
    <div v-if="filmArray.length > 0" class="sectionTitle">Film più votati su Boolflix</div>
    <!-- Horizontal Scroller -->
    <div class="row py-1 horizonal-scroll">     
      <div class="col" v-for="film in filmArray" :key="film.id">
        <FilmComponent :Film="film" :GenreFilmArray="GenreFilmArray"/>
      </div>
    </div>
    <!-- Section Name -->
    <div v-if="serieArray.length > 0" class="sectionTitle">Serie TV più votate su Boolflix</div>
    <!-- Horizontal Scroller -->
    <div class="row py-1 horizonal-scroll">
      <div class="col" 
      v-for="serie in serieArray" 
      :key="serie.id">
        <FilmComponent :Film="serie" :GenreFilmArray="GenreSerieArray"/>
      </div>
    </div>
  </div>
</template>

<script>
  // Import
  // import serieComponent from './serieComponent.vue';
  import FilmComponent from './FilmComponent.vue';
  
  export default {
    name: "BoolflixComponent",
    components: {
      FilmComponent,
      // serieComponent,
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
      font-size: 25px;
      margin: 10px 15px;
      font-weight: 600;
      text-transform: uppercase;
    }
    .col{
      padding-right: 0;
    }
    // setting horizontal scrolling
    .horizonal-scroll{
      height: calc(60% - 40px);
      flex-wrap: nowrap;
      overflow: auto;
      margin: 2px;
      
      // Scrollbar Modification
      &::-webkit-scrollbar {
        width: 10px;
        height: 8px;
      }
      &::-webkit-scrollbar-thumb:hover {
        background-color: grey;
      }
      &::-webkit-scrollbar-thumb {
        background-color: #333;
        border-radius: 20px;
        border: 6px solid transparent;
      }
    }
  }
</style>