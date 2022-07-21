<template>
    <div class="col-2 border border-dark">
    <div>
        Titolo:
        {{ singleMovie.title }}
    </div>
    <div>
        Titolo originale:
        {{ singleMovie.original_title }}
    </div>
    <div>
        Lingua:
        <span :class="flagPath(singleMovie.original_language)"></span>
        
    </div>
    <div>
        Voto: 
        {{ singleMovie.vote_average }}
    </div>
  </div>

</template>

<script>
export default {
    name: 'cardMovies',
    props: {
        singleMovie: Object,
    },
    methods:{
        flagPath: function(language){
            return `fi fi-${language}`
        },
    }
}
</script>

<style lang="scss">
@import '~flag-icons/css/flag-icons.css';

</style>