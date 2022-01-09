<template>
<ActorCard :actors="popularActors" />
</template>

<script>
import axios from 'axios'
export default {
 name: 'Actors',
  layout: 'CustomLayout',

  data () {
    return {
      popularActors: [],
    }
  },

   async fetch () {
    await this.getPopularActors()
  },

   methods: {

    async getPopularActors () {
        const data = axios.get(
        'https://api.themoviedb.org/3/person/popular?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US&page=1'
      )
      const result = await data
      let actors = result.data.results.slice(0,18)
      actors.forEach((actor) => {
        this.popularActors.push(actor)
      })
    },
  }
}
</script>
