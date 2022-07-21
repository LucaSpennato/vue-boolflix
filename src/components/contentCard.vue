<template>
    <ul class="col-2">
        <li>
            Titolo: {{ isTitleOrName(info) }}
        </li>
        <li>
            Titolo originale: {{ isOriginalTitleOrName(info) }}
        </li>
        <li>
            Lingua: <span>{{ info.original_language }} </span>
            <span :class="flagPath(info.original_language)"></span>
        </li>
        <li>
            Voto: {{ info.vote_average }}
        </li>
    </ul>

</template>

<script>
export default {
    name: 'tvShowCard',
    props: {
        info: Object,

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

        isTitleOrName: function(array){
            if(array.hasOwnProperty('title')){
                return array.title;
            }else{
                return array.name;
            }
        },

        isOriginalTitleOrName: function(array){
            if(array.hasOwnProperty('title')){
                return array.original_title;
            }else{
                return array.original_name;
            }
        }
    }
}
</script>

<style lang="scss">
@import '~flag-icons/css/flag-icons.css';

</style>