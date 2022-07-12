<template>
<header>
    <div>
        <h1>BoolFlix</h1>
    </div>
    <div class="search">
        <input type="text" placeholder="Cerca il film o la serie tv" v-model="searchtext">
        <button @click.prevent="searchName()">Submit</button>
    </div>
</header>
</template>

<script>
export default{
    name: "HeaderBoolfix",
    data(){
        return{
            searchtext: '',
        }
    },
    methods:{
        searchName(){
            if(this.searchtext !== ''){
                this.$emit("sendtext", this.searchtext);
                this.searchtext = "";
            }
        }
    }
}
</script>

<style lang="scss" scoped>
    header{
        height: 80px;
        background-color: black;
        display: flex;
        justify-content: center;
        justify-content: space-between;

        h1{
            text-transform: uppercase;
            font-size: 28px;
            padding: 0 40px;
            color: red;
        }

        .search{
            font-size: 20px;
            padding: 0 20px;
            margin: 5px 20px;
            outline: none;
        }

        button{
            font-size: 20px;
            padding: 1px 20px;
            border-radius: 6px;
            margin-left: 5px;
        }
    }
</style>