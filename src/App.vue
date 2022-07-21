<template>
  <div id="app">

    <Header @searchMovie="getMovie"/>
    <Main
    :contentResults="searchResults"
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
      searchResults: [],
      tvShow: [],
    }
  },

  methods:{

    getMovie: function(needle){

      if(needle !== undefined && needle !== ''){
        axios.get(`${this.getMovies}&query=${needle}`)
        .then((response)=>{
          this.searchResults = response.data.results;
          console.log(this.searchResults);
        })
        .catch((error)=>{
          console.warn(error);
        });
        axios.get(`${this.getSeries}&query=${needle}`)
        .then((seriesResponse)=>{
          this.tvShow = seriesResponse.data.results;
          console.warn(this.tvShow);
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
