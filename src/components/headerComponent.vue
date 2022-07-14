<template>
  <header>
    <div>
      <!-- Logo di Boolflix -->
      <img src="../assets/boolflixlogo.png" alt="">
      <!-- NAV menù -->
      <ul class="nav">
        <li>Home</li>
        <li>Serie TV</li>
        <li>Film</li>
        <li>Original</li>
        <li>Aggiunti di recente</li>
        <li>La mia lista</li>
      </ul>
    </div>
    <!-- Crezione dell side di ricerca -->
    <div class="inputs">
      <select @change="onChange($event)" name="select" id="select" >
        <option selected="selected" value="All">All</option>
        <option v-for="(Genre,index) in getAllGenre(this.GenreSerieArray,this.GenreFilmArray)" :key="index" :value="Genre.id">{{ Genre.name }}</option>
      </select> 
      <input type="text" placeholder="cerca" v-model="searchText">
      <button @click.prevent="sendSearchText()">submit</button>
    </div>
   
   
  </header>
</template>
  
<script>
export default {
  name: "HeaderComponent",
  props:{
    GenreSerieArray: Array,
    GenreFilmArray: Array,
  },
  data(){
    return{
      searchText: '',
    }
  },
  methods: {
    sendSearchText(){
      // controllo se la input non sia vuota
      if(this.searchText !== ''){
        // poi la mando ad App.vue
        this.$emit("sendText", this.searchText);
        this.searchText = "";
      }           
    },
    getAllGenre(GenreSerieArray,GenreFilmArray){
      let ArrayToFilter = [];
      let ArrayToFilters = [];
      GenreSerieArray.forEach(element => {
        if(!ArrayToFilters.includes(element.name)){
          ArrayToFilter.push(element);
          ArrayToFilters.push(element.name);
        }       
      });
      GenreFilmArray.forEach(element => {
        if(!ArrayToFilters.includes(element.name)){
          ArrayToFilter.push(element);
          ArrayToFilters.push(element.name);
        }   
      });
      
      return ArrayToFilter;
    },
    onChange(value){  
      const GenreValue = value.target.value;
      console.log(GenreValue)
      this.$emit("sendValue", GenreValue);
    }
  }
}
</script>

<style lang="scss" scoped>
  // Navbar Style
  header{
    height: 70px;
    background-color: #222;
    display: flex;
    justify-content: space-between;
    align-items: center;
    
    div{
      margin-left: 20px;  
      display: flex;
      
      img{
        width: 160px;
      }
      .nav{
        display: flex;
        list-style-type: none;
        align-items: center;
        padding: 10px;
        li{
          padding: 0 13px;
          font-size: 18px;
          &:hover{
            transform: scale(1.05);
            cursor: pointer;      
          }
        }      
      }
    }
    
    // Inputs Style
    .inputs{
      
      padding: 0 20px;
      
      input{
        font-size: 18px;
        padding: 0 10px;
        margin: 0 15px;
        outline: none;
      }
      button{
        font-size: 18px;
        padding: 1px 10px;
        border-radius: 5px;
      }
    }
  }
</style>