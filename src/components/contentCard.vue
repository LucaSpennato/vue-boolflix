<template>
    <div class="col-3 p-0 content-card mx-5 my-3">
        <div>
            <img :src="imgPath(info)" :alt="isTitleOrName(info) + '`s poster'"
            class="text-light">
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
            <li v-if="isOriginalTitleOrName(info) !== isTitleOrName(info)">
                <div class="headings">Titolo originale:</div>
                <div>
                    {{ isOriginalTitleOrName(info) }}
                </div>
            </li>
            <li>
                <div class="headings">Lingua originale:</div>
                <span :class="flagPath(info.original_language)"></span>
            </li>
            <li>
                <div class="headings">Voto:</div> 
                <span  v-for="star in 5" :key="star">
                    <i :class="parseVote(info) >= star ? 'bi bi-star-fill text-warning' : 'bi bi-star' "></i> 
                </span>
            </li>
            <li>
                <div>Cast:</div>
                <div 
                v-for="cast in casts" :key="cast.id">
                    {{ cast.name }}
                </div>
            </li>
            <li v-if="info.overview !== ''">
                <div class="headings">
                    Trama:
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
        casts: Array,
    },
    methods:{
        parseVote: function(Object){
            let vote = Math.ceil(Object.vote_average/2);
            return vote;
        },

        flagPath: function(language){
            if(language === 'en'){
                return `fi fi-us`;
            }else if(language == null || language == ''){
                return `fi fi-xx`;
            }else if(language == 'zh'){
                return `fi fi-cn`;
            }else if(language == 'ja'){
                return `fi fi-jp`;
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
            if(Object.poster_path !== null){
                return 'http://image.tmdb.org/t/p/w342/' + Object.poster_path;
            }else{
                // return 'http://www.travelettes.net/wp-content/uploads/2017/04/5004-432-840x1250.jpg';
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

        // .img-not-found-placeholder img{
        //     width: 100%;
        //     height: 100%;
        //     visibility: hidden;
        //     color: white;
        //     object-fit: cover;
        // };

        //  TODO sicuramente no, ma chiedi se un placeholder ha senso, probabilmente è più sensato lasciare l'alt
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