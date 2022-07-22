<template>
    <div class="col-3 p-0 content-card mx-5 my-3">
        <div>
            <img :src="imgPath(info)" :alt="isTitleOrName(info) + '`s poster'">
        </div>
        <ul class="text-light">
            <li>
                <div class="headings">
                    Titolo:
                </div>
                 <div>
                    {{ isTitleOrName(info) }}
                 </div>
            </li>
            <li>
                <div class="headings">Titolo originale:</div>
                <div>
                    {{ isOriginalTitleOrName(info) }}
                </div>
            </li>
            <li>
                <div class="headings">Lingua originale:</div>
                <span>{{ info.original_language }} </span>
                <span :class="flagPath(info.original_language)"></span>
            </li>
            <li>
                <div class="headings">Voto:</div> 
                <span  v-for="star in 5" :key="star">
                    <i :class="parseVote(info) >= star ? 'bi bi-star-fill text-warning' : 'bi bi-star' "></i> 
                </span>
            </li>
            <li>
                <div class="headings">
                    Overview:
                </div>
                <div>
                    {{ info.overview }}
                </div>
            </li>
        </ul>
    </div>

</template>

<script>
export default {
    name: 'tvShowCard',
    props: {
        info: {
            required: true,
            type: Object,
        },

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
                // TODO v-if se il contenuto che arriva è vuoto metti un'immagine di errore con classe
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
        
        .headings{
            font-weight: bold;
            font-size: 1.3rem;
        }

        img{
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: all 200ms linear;
        }

        ul{
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
            transition: all 200ms linear;
            opacity: 0;
            transform: rotateY(180deg);
            
            li{
                // font-size: 1.3rem;
                margin-bottom: .3rem;
            }
        }
        &:hover img{
            transform: rotateY(180deg);
            opacity: 0;
        }
        &:hover ul{
            transform: rotateY(0);
            opacity: 1;
        }

        ul::-webkit-scrollbar{
            width: .3rem;
        }
        ul::-webkit-scrollbar-thumb{
            background-color: white;
        }
    }

</style>