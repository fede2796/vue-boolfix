<template>
<div class="container">
    <div class="row row-cols-4 g-5">
        <div class="col" v-for="film in arrayFilm" :key="film.id" >
            <ComponentFilm :Film="film"/>
        </div>
    </div>
</div>
</template>

<script>
import ComponentFilm from "./ComponentFilm.vue";
export default{
    name:"FilmMain",
    components:{
        ComponentFilm,
    },
    props:{
        arrayFilm: Array,
    }
}
</script>

<style>
.container{
    padding-top: 50px;
}
</style>