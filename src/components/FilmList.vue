<template>
  <div class="container">
    <div class="row py-3">
        <div>
            Films:
        </div>
        <contentCard 
        v-for="singleMovie in moviesResults" :key="singleMovie.id"
        :info="singleMovie"
        />

    </div>
  </div>
</template>

<script>
import contentCard from '../components/contentCard.vue';

export default {
    name: 'FilmList',
    components:{
        contentCard,
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