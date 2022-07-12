<template>
  <div class="container">
    <div class="row row-cols-4 g-5">
      <div class="col" v-for="film in filmArray" :key="film.id">
        <ComponentFilm :Film="film"/>
      </div>
      <div class="col" v-for="serie in serieArray" :key="serie.id">
        <SerieComponent :Film="serie"/>
      </div>
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
    }
  }
</script>

<style lang="scss" scoped>
  .container{
    padding: 60px 0;
  }
</style>