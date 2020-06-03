<template>
  <div class="hello">
    <button @click="loadMovies">Load more</button>
    <div>
      <button @click="filter = 'movie'">Show movies</button>
      <button @click="filter = 'series'">Show series</button>
      <button @click="filter = ''">Show all</button>
    </div>
    <MovieListItem
      v-for="movie in filterMovies"
      :key="movie.imdbID"
      :movie="movie"
      />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import MovieService from '@/services/MovieService';
import { Movie } from '@/services/types';
import MovieListItem from './MovieListItem.vue';

export default Vue.extend({
  name: 'MovieList',
  data() {
    return {
      movies: [] as Movie[],
      filter: '',
    };
  },
  async created() {
    await this.loadMovies();
  },
  methods: {
    // dont know what other page should i load on load more, so ended up with duplicates
    async loadMovies(page = '273b9082') {
      const result = await MovieService.movieService
        .getMovieList(MovieService.movieService.myToken, page);
      this.movies = this.movies.concat(result.result);
    },
  },
  computed: {
    filterMovies(): any {
      if (this.filter) {
        return this.movies.filter((item) => item.Type === this.filter);
      }
      return this.movies;
    },
  },
  components: {
    MovieListItem,
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
