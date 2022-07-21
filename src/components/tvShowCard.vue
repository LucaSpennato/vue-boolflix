<template>
    <div class="col-2 border border-dark">
    <div>
        Titolo:
        {{ tvShow.name }}
    </div>
    <div>
        Titolo originale:
        {{ tvShow.original_title }}
    </div>
    <div>
        Lingua:
        <span>{{ tvShow.original_language }}</span>
        <span :class="flagPath(tvShow.original_language)"></span>
    </div>
    <div>
        Voto: 
        {{ tvShow.vote_average }}
    </div>
  </div>

</template>

<script>
export default {
    name: 'tvShowCard',
    props: {
        tvShow: Object,

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