<template>
    <ul class="col-2">
        <li>
            Titolo: {{ tvShow.name }}
        </li>
        <li>
            Titolo originale: {{ tvShow.original_title }}
        </li>
        <li>
            Lingua: <span>{{ tvShow.original_language }} </span>
            <span :class="flagPath(tvShow.original_language)"></span>
        </li>
        <li>
            Voto: {{ tvShow.vote_average }}
        </li>
    </ul>

</template>

<script>
export default {
    name: 'tvShowCard',
    props: {
        tvShow: Object,
        // TODO: chiedere se il required è effettivamente indispendabile ad ogni passaggio nonostante io lo abbia messo in principio ma non qua! SICURAMENTE SI
    },
    methods:{
        flagPath: function(language){
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