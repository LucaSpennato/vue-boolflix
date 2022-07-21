<template>
    <div class="col-2 border border-dark">
    <div>
        Titolo:
        {{ singleShow.title }}
    </div>
    <div>
        Titolo originale:
        {{ singleShow.original_title }}
    </div>
    <div>
        Lingua:
        <span :class="flagPath(singleShow.original_language)"></span>
    </div>
    <div>
        Voto: 
        {{ singleShow.vote_average }}
    </div>
  </div>

</template>

<script>
export default {
    name: 'cardMovies',
    props: {
        singleShow: Object,

    },
    methods:{
        flagPath: function(language){
            // TODO: chiedi se possa andar bene, altrimenti v-if con messaggio tipo: 'nessuna lingua'
            if(language === 'en'){
                return `fi fi-us`;
            }else if(language == null && language == '' && language == null){
                return `fi fi-xx`
            }else{
                return `fi fi-${language}`;
            }
        },
    }
}
</script>

<style lang="scss">
@import '~flag-icons/css/flag-icons.css';

</style>