<template>
  <div id="app">

    <Header @searchMovie="callParams"/>
    <Main
    :moviesResults="movies"
    :tvShowsRetults="tvShows"

    :moviecast="movieCast"
    :tvcast="tvCast"

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
      callUrl: 'https://api.themoviedb.org/3/search/',
      apiKey: '70b4d3b90fb8be81af37cad624a5b05b',
      movies: [],
      tvShows: [],
      areMoviesThere: null,
      areTvsThere: null,
      movieCast: [],
      tvCast: [],

    }
  },

  methods:{

    callParams: function(needle){
      const parameters= {
        params: {
          api_key: this.apiKey,
          language: 'it-IT',
          query: needle,
        }
      }
      console.log(parameters)
      if(needle !== undefined && needle !== null && needle !== ''){
        this.getMovie(parameters);
        this.getSeries(parameters);
      }
    },

    getMovie: function(apiParams){
      console.log(apiParams)
        axios.get(this.callUrl + 'movie', apiParams  )
        .then((response)=>{
          this.movies = response.data.results;
          console.log(this.movies);
          this.areMoviesFound();
          this.callMovieCast();
        })
        .catch((error)=>{
          console.warn(error);
        });
    },

    getSeries: function(apiParams){
      axios.get(this.callUrl + 'tv', apiParams)
      .then((response)=>{
          this.tvShows = response.data.results;
          console.log(this.tvShows);
          this.callTvCast()
          this.areTvsFound();
        })
        .catch((error)=>{
          console.warn(error);
        });
    },

    callMovieCast: function(){
      this.movies.forEach(element => {
      axios.get('https://api.themoviedb.org/3/movie/'+ element.id +'/credits?api_key=70b4d3b90fb8be81af37cad624a5b05b')
      .then((response)=>{
      this.movieCast = response.data.cast
      this.movieCast = this.movieCast.slice(0,5)
      console.log(this.movieCast);
      })
      .catch((error)=>{
      console.warn(error);
      });
      })
    },

    callTvCast: function(){
      this.tvShows.forEach(element => {
      axios.get('https://api.themoviedb.org/3/tv/'+ element.id +'/credits?api_key=70b4d3b90fb8be81af37cad624a5b05b')
      .then((response)=>{
      this.tvCast = response.data.cast
      this.tvCast = this.tvCast.slice(0,5)
      console.warn(this.tvCast);
      })
      .catch((error)=>{
      console.warn(error);
      });
      })
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
