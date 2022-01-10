<template>
<div>
  	<input class="header__search-input"
                type="text"
                placeholder="Search Movies"
                @keyup.enter="$fetch"
                v-model.lazy="searchInput"
                >
  <br>
     <div v-show="$fetchState.pending" class="mt-1" style="position: fixed; color: white">Searching.... </div>
     <!-- <div v-if="$fetchState.pending" class="mt-1" style="position: fixed; color: white">Searching.... </div> -->
   <div v-if="searchedMovies.length && searchInput !== ''" class="list-item mt-3" style="position: absolute; background-color: #1a191f; border-radius: 3px">
               <ul  v-for="(movie, index) in searchedMovies" :key="index">
                <li class="show py-2" style="border-bottom: 1px solid gray">
              <NuxtLink
               :to="`/movies/${movie.id}`"
            >
                      	<img v-if="movie.poster_path" :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="poster" style="width: 14%" class="py-2 pl-3">
                        <img v-else src="https://via.placeholder.com/27x35" alt="poster" class="py-2 pl-3">
                    <span class="ml-4" style="text-align: left; color: white">{{ movie.title.slice(0, 25)}}</span>
                 </NuxtLink>
                </li>
               </ul>

          <div v-show="searchInput !== '' && !searchedMovies.length" class="list-item" style="color: white">No results for {{ searchInput }}</div>
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'SearchDropdown',

   data () {
    return {
      searchedMovies: [],
      searchInput: ''
    }
  },

    async fetch() {

    if (this.searchInput !== '') {
      await this.searchMovies()
    }

  },

  fetchDelay: 2000,

  watch: {
    // searchInput () {
    //   console.log(this.searchInput)
    // }
  },

   methods: {

    async searchMovies () {
      const data = axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1&query=${this.searchInput}`
      )
      const result = await data
      console.log(result.data)
      movies = result.data.results.slice(0,7)
      movies.forEach((movie) => {
        this.searchedMovies.push(movie)
      })
    },

    // clearSearch () {
    //   this.searchInput = ''
    //   this.searchedMovies = []
    // }
  }
}
</script>
