<template>
  <main class="bg-dark">
    <div v-if="isMovie == null && isTv== null" class="fs-1 text-center text-light p-5">
        Comincia la tua ricerca!
    </div>
    <div v-else-if="isMovie || isTv">
      <FilmList :moviesResults="moviesResults" v-if="isMovie"/>
      <TvShowList :tvShowsRetults="tvShowsRetults" v-if="isTv"/>
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

        tvShowsRetults:{
          required: true,
          type: Array,
        },

        isMovie: Boolean,
        isTv: Boolean,
    }
}
</script>

<style lang="scss">

  main{
    min-height: calc(100vh - 4rem)
  }
</style>