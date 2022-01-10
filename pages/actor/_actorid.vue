<template>
<div>

<Loading v-if="$fetchState.pending" />
<div v-else>
<section class="section section--details section--bg" data-bg="">
    <!-- details content -->
    <div class="container">
        <div class="row">
<div class="col-12 col-lg-3">
<div class="card__cover">
    <img :src="`https://image.tmdb.org/t/p/w500/${actor.profile_path}`" alt="">
</div>
</div>
<div class="col-12 col-lg-1">
</div>
            <!-- content -->

            <div class="col-12 col-lg-8">
                <div class="card card--details">
                        <!-- title -->
            <h1 class="section__title">{{ actor.name }}</h1>
            <!-- end title -->
                    <div class="row">
                    <!-- card content -->
                        <div class="col-12 col-sm-7 col-lg-6 col-xl-12">
                            <div class="card__content">
                                <ul class="card__meta">
                                    <li>Country: <span class="ml-3" style="color: #ffd80e">{{ actor.place_of_birth }}</span></li>
                                    <li>Date of Birth: <span class="ml-3" style="color: #ffd80e">
                                      {{
                                        new Date(actor.birthday).toLocaleString('en-us', {
                                          month: 'long',
                                          day: 'numeric',
                                          year: 'numeric',
                                        })
                                      }}
                                      </span></li>
                                    <li>Age: <span class="ml-3" style="color: #ffd80e"> {{ calculateAge(actor.birthday) }} years old</span></li>
                                </ul>
                                <div class="card__description">
                                    {{ actor.biography }}
                                </div>
                            </div>
                        </div>
                        <!-- end card content -->
                    </div>
<br>
                    <div class="row">
                        <!-- card content -->
                            <div class="col-12 col-sm-7 col-lg-6 col-xl-12">
                                <div class="card__content">
                                    <ul class="card__meta">
                                        <li>Known For</li>

                                    </ul>
                                    <br>
                                    <div class="row">
                                     <div class="col-6 col-sm-4 col-md-3 col-xl-2" v-for="(known, index) in knownFor" :key="index">
                                            <div class="card">
                                                <div class="card__cover">
                                                   <NuxtLink
                                                       :to="`/${known.media_type}/${known.id}`"
                                                        >
                                                       <img :src="`https://image.tmdb.org/t/p/w500/${known.poster_path}`" alt="" style="width: 100%">
                                                        </NuxtLink>
                                                </div>
                                                <div class="card__content">
                                                    <span class="card__category" >
                                                        <NuxtLink style="color: #ffd80e"
                                                       :to="`/${known.media_type}/${known.id}`"
                                                        >
                                                        {{ known.original_name ? known.original_name : known.original_title }}
                                                        </NuxtLink>
                                                    </span>
                                                </div>
                                            </div>
                                        </div>
                                         </div>
                                </div>
                            </div>
                            <!-- end card content -->
                        </div>
                </div>
            </div>
            <!-- end content -->
        </div>
    </div>
</section>
<div class="container mb-4">
        <div class="col-12 mb-4">
            <h2 class="content__title">Credits</h2>
        </div>
            <div class="col-12 col-sm-6 col-md-6 col-xl-6" v-for="(credit, index) in credits" :key="index">
                <h3 class="card__title"><li>  {{
                                        new Date(credit.release_date ? credit.release_date : credit.first_air_date).toLocaleString('en-us', {
                                          year: 'numeric', })
                                      }} -
                  <strong>
                    <NuxtLink
                    class="hover:underline"
                    :to="`/${credit.media_type}/${credit.id}`">
                    {{ credit.original_title ? credit.original_title : credit.original_name }}
                    </NuxtLink>
                  </strong> as {{ credit.character }}</li></h3>
            </div>
</div>
</div>
</div>
</template>

<script>
import axios from 'axios'
export default {
 name: 'singleActor',
  layout: 'CustomLayout',

  data() {
    return {
      actor: null,
      credits: [],
      knownFor: [],
      credits: []
    }
  },

   async fetch() {
    await this.getSingleActor()
    await this.getCredits()
  },

 fetchDelay: 2000,

  methods: {
      async getSingleActor() {
      const data = axios.get(
        `https://api.themoviedb.org/3/person/${this.$route.params.actorid}?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US`
      )
      const result = await data
      this.actor = result.data
    },

    async getCredits() {
    const data = axios.get(
        `https://api.themoviedb.org/3/person/${this.$route.params.actorid}/combined_credits?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US`
      )
      const result = await data
      let credits = result.data.cast
      this.knownFor = credits.slice(0,6)
      this.credits = credits
    },

    calculateAge (date){
      let currentDate =  new Date().toLocaleString('en-us', { year: 'numeric', })
      let birthday = new Date(date).toLocaleString('en-us', { year: 'numeric', })
      let age = currentDate - birthday;
      return age
    }
  }
}
</script>
