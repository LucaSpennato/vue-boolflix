<template>
    <ul class="col-2">
        <li>
            Titolo: {{ movie.title }}
        </li>
        <li>
            Titolo originale: {{ movie.original_title }}
        </li>
        <li>
            Lingua: <span>{{ movie.original_language }} </span>
            <span :class="flagPath(movie.original_language)"></span>
        </li>
        <li>
            Voto: {{ movie.vote_average }}
        </li>
    </ul>

</template>

<script>
export default {
    name: 'cardMovies',
    props: {
        movie: Object,

    },
    methods:{
        flagPath: function(language){
            // TODO: chiedi se possa andar bene, altrimenti v-if con messaggio tipo: 'nessuna lingua'
            if(language === 'en'){
                return `fi fi-us`;
            }else if(language == null || language == '' || language == null || language == 'zh'){
                return `fi fi-xx`;
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