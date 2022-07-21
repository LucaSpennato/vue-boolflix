<template>
  <header class="bg-dark">
    <div class="container">
        <div class="row p-2 text-center">
            <nav class="col-12">
                <input type="text" v-model="searchInput">
                <button class="btn btn-primary"
                @click="sendInput()"
                >cerca</button>
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

<style>

</style>