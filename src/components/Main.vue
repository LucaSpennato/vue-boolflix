<template>
  <main class="bg-dark">
    <div v-if="areMoviesFound === null && areTvsFound === null" class="fs-1 text-center text-light p-5">
        Comincia la tua ricerca!
    </div>
    <div v-else-if="areMoviesFound || areTvsFound">

      <FilmList :moviesResults="moviesResults"
       :moviecast="moviecast"
       v-if="areMoviesFound"/>

      <TvShowList :tvShowsRetults="tvShowsRetults"
        :tvcast="tvcast"
       v-if="areTvsFound"/>
    </div>
    <div v-else class="fs-1 text-center text-light p-5">
      Nessun risultato
    </div>
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

        moviecast: Array,
        tvcast: Array,

        tvShowsRetults:{
          required: true,
          type: Array,
        },

        areMoviesFound: Boolean,
        areTvsFound: Boolean,
    },
}
</script>

<style lang="scss">

  main{
    min-height: calc(100vh - 4rem)
  }
</style>