<template>
  <div class="container">
    <div class="row py-3">
        <div class="text-white fs-1 mb-2">
            Tv Shows:
        </div>
        <contentCard 
        v-for="singleTvShow in tvShowsRetults" :key="singleTvShow.id"
        :info="singleTvShow"
        :casts="tvcast"
        
        />
    </div>
  </div>
</template>

<script>
import contentCard from '../components/contentCard.vue';

export default {
    name: 'TvShowList',
    components:{
        contentCard,
    },
    props:{
        tvShowsRetults:{
          required: true,
          type: Array,
        },
        tvcast: Array,
    },
}
</script>

<style>

</style>