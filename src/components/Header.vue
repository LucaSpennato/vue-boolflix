<template>
  <header>
    <div class="container">
        <div class="row p-2 text-center justify-content-between">
            <div class="col-2 fs-2 text-danger fw-bold title">
                <img :src="require(`../assets/2273601509b2826c276835ecc910c578.png`)" 
                
                alt="boolflix-page-logo">
            </div>
            <nav class="col-4 d-flex align-items-center">
                <input type="text" v-model="searchInput"
                @keyup.enter="sendInput()">

                <button class="btn btn-danger mx-3 fw-bold"
                @click="sendInput()"
                >Cerca</button>
            </nav>
        </div>
    </div>
  </header>
</template>

<script>

export default {
    name: 'headercomponent',
    data: function(){
        return{
            searchInput: '',
        }
    },

    methods:{
        sendInput: function(){
            this.$emit('searchMovie', this.searchInput)
        }
    }, 
}
</script>

<style lang="scss">
// @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');
/* TODO: se sarà possibile aggiungi trim o comunque una verifica sulla stringa */
    header{
        background-color: black;
        height: 4rem;

        .title img{
            height: 2.5rem;
        }
    }
</style>