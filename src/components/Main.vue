<template>
  <main>
    <div class="container">
      <div class="row">
        <movieCard 
        v-for="movie in movies" :key="movie.id"
        :singleMovie="movie"
        />
      </div>
    </div>
  </main>
</template>

<script>
import movieCard from '../components/movieCard.vue';

export default {
    name: 'MainComponent',
    components:{
      movieCard,
    },
    props:{
        movies: Array,
    }
}
</script>

<style>

</style>