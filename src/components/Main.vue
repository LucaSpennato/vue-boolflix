<template>
  <main>
    <div class="container">
      <div class="row">
        <movieCard 
        v-for="show in contentResults" :key="show.id"
        :singleShow="show"
        />
      </div>
    </div>
  </main>
</template>

<script>
import movieCard from '../components/movieCard.vue';

export default {
    name: 'MainComponent',
    components:{
      movieCard,
    },
    props:{
        contentResults: {
          required: true,
          type: Array,
        },
    }
}
</script>

<style>

</style>