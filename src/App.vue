<template>
  <div id="app">

    <Header @searchMovie="getMovie"/>
    <Main
    :movies="movies"
    />

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
      apiCall: 'https://api.themoviedb.org/3/search/movie/?api_key=70b4d3b90fb8be81af37cad624a5b05b',
      movies: [],
    }
  },

  methods:{

    getMovie: function(needle){

      if(needle !== undefined && needle !== ''){
        axios.get(`${this.apiCall}&query=${needle}`)
        .then((response)=>{
          this.movies = response.data.results;
          console.log(this.movies)
        })
        .catch((error)=>{
          console.warn(error);
        })
      }
    }
  },
  created(){
    this.getMovie();
  }
}
</script>

<style lang="scss">
  @import '~bootstrap/scss/bootstrap.scss';

</style>
