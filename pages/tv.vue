<template>
<div>
  <!-- Shows Airing Today -->
    <section class="content" style="margin-top: 100px">
           <TvSection :title="`Shows Airing Today`"/>
          <TvCard :tvs="showsAiringToday" />
    </section>
    <!-- Shows Airing Today -->

     <!-- Shows On Air -->
    <section class="content">
           <TvSection :title="`Shows On Air`"/>
          <TvCard :tvs="showsOnAir" />
    </section>
    <!-- Shows On Air -->

    <!-- Popular Shows -->
    <section class="content">
           <TvSection :title="`Popular Shows`"/>
          <TvCard :tvs="popularShows" />
    </section>
    <!-- Popular Shows -->

    <!-- Top Rated Shows -->
    <section class="content">
           <TvSection :title="`Top Rated Shows`"/>
          <TvCard :tvs="topRatedShows" />
    </section>
    <!-- Top Rated Shows -->
</div>
</template>

<script>
import axios from 'axios'
export default {
 name: 'Tv',
  layout: 'CustomLayout',


  data () {
    return {
      tvGenres: [],
      showsAiringToday: [],
      showsOnAir: [],
      popularShows: [],
      topRatedShows: [],
    }
  },

  async fetch () {

    await this.getTvGenres()

    await this.getShowsAiringToday()

    await this.getShowsOnAir()

    await this.getPopularShows()

    await this.getTopRatedShows()
  },

  methods: {

     async getTvGenres () {
        const data = axios.get(
        'https://api.themoviedb.org/3/genre/tv/list?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US'
      )
      const result = await data
      result.data.genres.forEach((genre) => {
        this.tvGenres.push(genre)
      })
    },

    async getShowsAiringToday () {
      const data = axios.get(
        'https://api.themoviedb.org/3/tv/airing_today?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1'
      )
      const result = await data
      let mappedData = this.mapTvArray(result.data.results)
      mappedData.forEach((show) => {
        this.showsAiringToday.push(show)
      })
    },

    async getShowsOnAir () {
        const data = axios.get(
        'https://api.themoviedb.org/3/tv/on_the_air?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1'
      )
      const result = await data
      let mappedData = this.mapTvArray(result.data.results)
      mappedData.forEach((show) => {
        this.showsOnAir.push(show)
      })
    },

    async getPopularShows () {
      const data = axios.get(
        'https://api.themoviedb.org/3/tv/popular?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1'
      )
      const result = await data
      let mappedData = this.mapTvArray(result.data.results)
      mappedData.forEach((show) => {
        this.popularShows.push(show)
      })
    },

    async getTopRatedShows () {
      const data = axios.get(
        'https://api.themoviedb.org/3/tv/top_rated?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1'
      )
      const result = await data
      let mappedData = this.mapTvArray(result.data.results)
      mappedData.forEach((show) => {
        this.topRatedShows.push(show)
      })
    },

    mapTvArray (tvs) {

      return tvs.map(obj => ({
        id: obj.id,
        name: obj.name,
        poster_path: obj.poster_path,
        genres: this.getConvertedGenres(obj.genre_ids),
        vote_average: obj.vote_average,
      }));
      
    },

    getConvertedGenres (array) {
      let genres = [];
      array.forEach(id => {
        let genre = this.tvGenres.filter(test => test.id == id)[0].name;
        genres.push(genre)
      })
     return genres;
    }
  }
}
</script>
