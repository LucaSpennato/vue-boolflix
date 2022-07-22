<template>
    <div class="col-3 p-0 content-card mx-5 my-3">
        <div>
            <img :src="imgPath(info)" :alt="isTitleOrName(info) + '`s poster'">
        </div>
        <ul class="text-light">
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
                Voto: 
                <span  v-for="star in 5" :key="star">
                    <i :class="parseVote(info) >= star ? 'bi bi-star-fill text-warning' : 'bi bi-star' "></i> 
                </span>
            </li>
            <li>
                Overview: {{ info.overview }}
            </li>
        </ul>
    </div>

</template>

<script>
export default {
    name: 'tvShowCard',
    props: {
        info: Object,

        // TODO: chiedere se il required è effettivamente indispendabile ad ogni passaggio nonostante io lo abbia messo in principio ma non qua! SICURAMENTE SI
    },
    methods:{

        parseVote: function(Object){
            let vote = Math.ceil(Object.vote_average/2);
            return vote;
        },

    // FIXME Chiedi consiglio su come sistemare!
        flagPath: function(language){
            if(language === 'en'){
                return `fi fi-us`;
            }else if(language == null || language == '' || language == 'zh'){
                return `fi fi-xx`;
            }else{
                return `fi fi-${language}`;
            }
        },

        isTitleOrName: function(Object){
            if(Object.hasOwnProperty('title')){
                return Object.title;
            }else{
                return Object.name;
            }
        },

        isOriginalTitleOrName: function(Object){
            if(Object.hasOwnProperty('title')){
                return Object.original_title;
            }else{
                return Object.original_name;
            }
        },

        imgPath: function(Object){
            if(Object.backdrop_path !== null){
                return 'http://image.tmdb.org/t/p/w342/' + Object.poster_path;
            }else{
                return '';
            }
        },
    }
}
</script>

<style lang="scss">
@import '~flag-icons/css/flag-icons.css';
@import '~bootstrap-icons/font/bootstrap-icons.css';

    .content-card{
        position: relative;
        border: 2px solid white;

        img{
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        ul{
            display: none;
            list-style: none;
            position: absolute;
            height: 100%;
            width: 100%;
            padding:  .5rem 1rem 0;
            z-index: 1;
            top: 0;
            left: 0;
            overflow: auto;
            background-color: black;
            
            li{
                font-size: 1.3rem;
            }
        }

        &:hover ul{
            display: block;
        }

        ul::-webkit-scrollbar{
            width: .3rem;
        }
        ul::-webkit-scrollbar-thumb{
            background-color: white;
        }
    }

</style>