<template>
  <div class="container">
    <div class="row py-3">
        <div>
            Tv Shows:
        </div>
        <tvShowCard 
            v-for="singleTvShow in tvShowsRetults" :key="singleTvShow.id"
            :tvShow="singleTvShow"
        />
    </div>
  </div>
</template>

<script>
import tvShowCard from '../components/tvShowCard.vue';

export default {
    name: 'TvShowList',
    components:{
        tvShowCard,
    },
    props:{
        tvShowsRetults:{
          required: true,
          type: Array,
        },
    }
}
</script>

<style>

</style>