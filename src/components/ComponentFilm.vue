<template>
<div class="film">
    <div>
        <span>{{Film.image}}</span>
    </div>
    <div>
        <span>{{Film.title}}</span>
    </div>
     <div>
        <span>{{Film.original_title}}</span>
    </div>
     <div>
        <span>{{Film.original_language }}</span>
    </div>
     <div>
        <span>{{Film.vote_average }}</span>
    </div>
</div>
</template>

<script>
 export default{
    name:"ComponentFilm",
    props:{
        Film:Object,
    }
 }
</script>

<style lang="scss" scoped>
    .film{
        padding: 10px;
        border: 1px solid red;
        height: 100%;

        div{
            text-align: center;
            text-transform: uppercase;
        }
    }

</style>