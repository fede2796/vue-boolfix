<template>
  <header>
    <div>
      <h1>boolflix</h1>
    </div>
    <div class="inputs"> 
      <input type="text" placeholder="cerca" v-model="searchText">
      <button @click.prevent="sendSearchText()">submit</button>
    </div>
   
  </header>
</template>

<script>
export default {
  name: "HeaderBoolfix",
  data(){
    return{
      searchText: '',
    }
  },
  methods: {
    sendSearchText(){
      if(this.searchText !== ''){
        this.$emit("sendText", this.searchText);
        this.searchText = "";
      }           
    }
  }
}
</script>

<style lang="scss" scoped>
  header{
    height: 70px;
    background-color: black;
    display: flex;
    justify-content: space-between;
    align-items: center;
    h1{
      text-transform: uppercase;
      font-size: 25px;
      padding: 0 20px;
      color: red;
    }
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