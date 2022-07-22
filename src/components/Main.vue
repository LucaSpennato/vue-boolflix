<template>
  <main class="bg-dark">
    <FilmList :moviesResults="moviesResults"/>
    <TvShowList :tvShowsRetults="tvShowsRetults"/>
  </main>
</template>

<script>

import FilmList from '../components/FilmList.vue';
import TvShowList from '../components/TvShowList.vue';




export default {
    name: 'MainComponent',
    components:{
      FilmList,
      TvShowList,
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

<style lang="scss">

  main{
    min-height: calc(100vh - 4rem)
  }

/* TODO: chiedere se posso aggiungere una verifica v-if="moviesResults.length > 0" in caso di elementi mancanti ed anche un loader! */
</style>