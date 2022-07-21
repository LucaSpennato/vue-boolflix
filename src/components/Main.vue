<template>
  <main>
    <div class="container">
      <div class="row py-3">
        <div>Movies:</div>
        <movieCard 
        v-for="singleMovie in moviesResults" :key="singleMovie.id"
        :movie="singleMovie"
        />
      </div>
      <div class="row py-3">
        <div>tv shows:</div>
        <tvShowCard 
        v-for="singleTvShow in tvShowsRetults" :key="singleTvShow.id"
        :tvShow="singleTvShow"
        />
      </div>
    </div>
  </main>
</template>

<script>
import movieCard from '../components/movieCard.vue';
import tvShowCard from '../components/tvShowCard.vue';


export default {
    name: 'MainComponent',
    components:{
      movieCard,
      tvShowCard,
    },
    props:{
        moviesResults: {
          required: true,
          type: Array,
        },
        tvShowsRetults:{
          required: true,
          type: Array,
        },
    }
}
</script>

<style>
/* TODO: chiedere se posso aggiungere una verifica v-if="moviesResults.length > 0" in caso di elementi mancanti ed anche un loader! */

</style>