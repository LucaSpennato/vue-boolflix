<template>
  <div id="app">

    <Header @searchMovie="getMovie"/>
    <Main
    :moviesResults="movies"
    :tvShowsRetults="tvShows"
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
      getMovies: 'https://api.themoviedb.org/3/search/movie/?api_key=70b4d3b90fb8be81af37cad624a5b05b',
      getSeries: 'https://api.themoviedb.org/3/search/tv/?api_key=70b4d3b90fb8be81af37cad624a5b05b',
      movies: [],
      tvShows: [],
    }
  },

  methods:{

    getMovie: function(needle){

      if(needle !== undefined && needle !== ''){
        axios.get(`${this.getMovies}&query=${needle}`)
        .then((response)=>{
          this.movies = response.data.results;
          console.log(this.movies);
          // TODO sistemare gli oggetti in ordine di id
        })
        .catch((error)=>{
          console.warn(error);
        });
        axios.get(`${this.getSeries}&query=${needle}`)
        .then((seriesResponse)=>{
          this.tvShows = seriesResponse.data.results;
          // console.warn(this.tvShows);
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
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Montserrat:wght@300;400;500;700&display=swap');

  *{
    font-family: 'Bebas Neue', cursive;
    font-family: 'Montserrat', sans-serif;
  }

</style>
