<template>
  <div class="container">
    <div class="row py-3">
        <div>
            Tv Shows:
        </div>
        <contentCard 
        v-for="singleTvShow in tvShowsRetults" :key="singleTvShow.id"
        :info="singleTvShow"
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
    }
}
</script>

<style>

</style>