<template>
  <div class="film">
    <div><span>Titolo: </span>{{ Film.name }}</div>
    <div><span>Titolo originale: </span>{{ Film.original_name }}</div>
    <div><span>voto: </span>{{ Film.vote_average }}</div>
    <div><span>{{ Film.original_language }}</span><img :src="getFlags(Film.original_language)" alt="dd"></div>
    
    <div class="fleg"></div>
  </div>
</template>

<script>
export default {
  name: "FilmComponent",
  props:{
    Film:Object,
  },
  methods:{    
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
      }  else if(nazionalita == 'zh'){
        nazionalita = "cn";
      }
      return `https://countryflagsapi.com/png/${nazionalita}`;
    }
  }
}
</script>
 
<style lang="scss" scoped>
  .film{
    padding: 5px;
    border: 1px solid white;
    height: 100%;
    div{
      text-transform: uppercase;
      padding: 5px 0;
      span{
        font-weight: 800;
      }
    }
    img{
      width: 30px;
      height: 20px;
      display: inline;
      margin: 0 10px;
    }
  }
</style>