<template>
  <div class="movie-view">
    <h1>{{movieData.Title}}</h1>
    <img :src="movieData.Poster" alt="">
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import MovieService from '@/services/MovieService';

export default Vue.extend({
  name: 'MovieView',
  props: {
    movieId: String,
  },
  data() {
    return {
      movieData: {},
    };
  },
  async created() {
    this.movieData = await MovieService.movieService
      .getSpecificMovie(MovieService.movieService.myToken, this.$route.params.movieId);
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
