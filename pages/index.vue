<template>
  <div>
    <!-- Upcoming Movies -->
    <section class="content" style="margin-top: 100px">
           <MovieSection :title="`Upcoming Movies`"/>
          <MovieCard :movies="upcomingMovies" />
    </section>
    <!-- Upcoming Movies -->

    <!-- Popular Movies -->
    <section class="content">
     <MovieSection :title="`Popular Movies`"/>
      <MovieCard :movies="popularMovies" />
    </section>
    <!-- Popular Movies -->

    <!-- Top Rated Movies -->
    <section class="content">
     <MovieSection :title="`Top Rated Movies`"/>
      <MovieCard :movies="topRatedMovies" />
    </section>
    <!-- Top Rated Movies -->

    <!-- Now Playing Movies -->
    <section class="content">
   <MovieSection :title="`Now Playing`"/>
      <MovieCard :movies="nowPlayingMovies" />
    </section>
    <!-- Now Playing Movies -->
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Home',
  layout: 'CustomLayout',

  data () {
    return {
      upcomingMovies: [],
      popularMovies: [],
      topRatedMovies: [],
      nowPlayingMovies: [],
    }
  },

  async fetch () {

    await this.getUpcomingMovies()

    await this.getPopularMovies()

    await this.getTopRatedMovies()

    await this.getNowPlayingMovies()

  },

  methods: {
    async getUpcomingMovies () {
      const data = axios.get(
        'https://api.themoviedb.org/3/movie/upcoming?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1'
      )
      const result = await data
      result.data.results.forEach((movie) => {
        this.upcomingMovies.push(movie)
      })
    },

    async getPopularMovies () {
        const data = axios.get(
        'https://api.themoviedb.org/3/movie/popular?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1'
      )
      const result = await data
      result.data.results.forEach((movie) => {
        this.popularMovies.push(movie)
      })
    },

    async getTopRatedMovies () {
      const data = axios.get(
        'https://api.themoviedb.org/3/movie/top_rated?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1'
      )
      const result = await data
      result.data.results.forEach((movie) => {
        this.topRatedMovies.push(movie)
      })
    },

    async getNowPlayingMovies () {
      const data = axios.get(
        'https://api.themoviedb.org/3/movie/now_playing?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1'
      )
      const result = await data
      result.data.results.forEach((movie) => {
        this.nowPlayingMovies.push(movie)
      })
    },
  }
}
</script>
