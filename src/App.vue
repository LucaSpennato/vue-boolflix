<template>
  <div id="app">

    <Header/>
    <Main/>

  </div>
</template>

<script>
import Main from './components/Main.vue';
import Header from './components/Header.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
  data: function(){
    return{
      call: 'https://api.themoviedb.org/3/movie/550?api_key=70b4d3b90fb8be81af37cad624a5b05b',
    }
  },

  methods:{
    getStuff: function(){
      axios.get(this.call)
      .then((response)=>{
        console.log(response);
      })
      .catch((error)=>{
        console.warn(error);
      })
    }
  },
  created(){
    this.getStuff();
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
