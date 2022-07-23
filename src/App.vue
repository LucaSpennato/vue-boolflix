<template>
  <div id="app">

    <Header @searchMovie="getMovie"/>
    <Main
    :moviesResults="movies"
    :tvShowsRetults="tvShows"

    :areMoviesFound="areMoviesThere"
    :areTvsFound="areTvsThere"
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
      getMovies: 'https://api.themoviedb.org/3/search/movie/',
      getSeries: 'https://api.themoviedb.org/3/search/tv/',
      apiKey: 'api_key=70b4d3b90fb8be81af37cad624a5b05b',
      movies: [],
      tvShows: [],
      areMoviesThere: null,
      areTvsThere: null,
    }
  },

  methods:{

    getMovie: function(needle){

      if(needle !== undefined && needle !== null && needle !== ''){
        axios.get(`${this.getMovies}?${this.apiKey}&query=${needle}`)
        .then((response)=>{
          this.movies = response.data.results;
          console.log(this.movies);
          this.areMoviesFound()
        })
        .catch((error)=>{
          console.warn(error);
        });
        axios.get(`${this.getSeries}?${this.apiKey}&query=${needle}`)
        .then((seriesResponse)=>{
          this.tvShows = seriesResponse.data.results;
          this.areTvsFound()
        })
      }
    },

    areMoviesFound: function(){
      
      if(this.movies.length === 0){
        return this.areMoviesThere = false;
      }else{
        return this.areMoviesThere = true;
      }
    },

    areTvsFound: function(){
      
      if(this.tvShows.length === 0){
        return this.areTvsThere = false;
      }else{
        return this.areTvsThere = true;
      }
    },

  },
  created(){
    this.getMovie();
  },
}
</script>

<style lang="scss">
  @import '~bootstrap/scss/bootstrap.scss';
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Montserrat:wght@300;400;500;700&display=swap');

  *{
    font-family: 'Bebas Neue', cursive;
    font-family: 'Montserrat', sans-serif;
  }
// TODO sistemare gli oggetti in ordine di id
</style>
