<template>
  <div class="container">
    <div class="row py-3">
        <div>
            Films:
        </div>
        <movieCard 
            v-for="singleMovie in moviesResults" :key="singleMovie.id"
            :movie="singleMovie"
            />

    </div>
  </div>
</template>

<script>
import movieCard from '../components/movieCard.vue';

export default {
    name: 'FilmList',
    components:{
        movieCard,
    },
    props:{
        moviesResults: {
          required: true,
          type: Array,
        },
    }
}
</script>

<style>

</style>