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
                                    <li>Date of Birth: <span class="ml-3" style="color: #ffd80e">{{ actor.birthday }}</span></li>
                                    <li>Age: <span class="ml-3" style="color: #ffd80e">{{ actor.age }} years old</span></li>
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
                                     <div class="col-6 col-sm-4 col-md-3 col-xl-2">
                                            <div class="card">
                                                <div class="card__cover">
                                                    <a href=""><img src="" alt="" style="width: 100%"></a>
                                                </div>
                                                <div class="card__content">
                                                    <span class="card__category" >
                                                        <a href="" style="color: #ffd80e"></a>
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
    }
  },

   async fetch() {
    await this.getSingleActor()
    await this.getCredits()
    await this.getKnownFor()
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
        `https://api.themoviedb.org/3/person/${this.$route.params.tvid}/credits?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US`
      )
      const result = await data
    },
  }
}
</script>
