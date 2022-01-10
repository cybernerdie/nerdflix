<template>
<div>

<Loading v-if="$fetchState.pending" />
<div v-else>
<section class="section section--details section--bg" data-bg="">
    <!-- details content -->
    <div class="container">
        <div class="row">

<!-- player -->
<div class="col-12 col-lg-3 mb-4">
<div class="card__cover">
    <img :src="`https://image.tmdb.org/t/p/w500/${tv.poster_path}`" alt="">
    <span class="card__rate card__rate--green">{{ tv.vote_average * 10}}%</span>
</div>
</div>

<div class="col-12 col-lg-1">
</div>
<!-- end player -->
            <!-- content -->

            <div class="col-12 col-lg-8">
                <div class="card card--details">
                        <!-- title -->
            <h1 class="section__title">{{tv.name}}</h1>
            <!-- end title -->
                    <div class="row">
                    <!-- card content -->
                        <div class="col-12 col-sm-7 col-lg-6 col-xl-12">
                            <div class="card__content">
                                <ul class="card__meta">
                                    <li>First Air Date: <span class="ml-3" style="color: #ffd80e">{{
                                        new Date(tv.first_air_date).toLocaleString('en-us', {
                                          month: 'long',
                                          day: 'numeric',
                                          year: 'numeric',
                                        })
                                      }}</span></li>
                                    <li>Genres: <span class="ml-3" style="color: #ffd80e">{{ genres.join(' , ') }}</span></li>

                                </ul>
                                <div class="card__description">
                                 {{ tv.overview}}
                                </div>
                            </div>
                        </div>
                        <!-- end card content -->
                    </div>
<br>
                    <div class="row">
                        <!-- content -->
                            <div class="col-12 col-sm-7 col-lg-12 col-xl-12">
                                <div class="card__content">
                                    <ul class="card__meta">
                                        <li>Featured Crew</li>

                                    </ul>
                                    <br>
                                    <div class="row">
                                        <div class="col-12 col-lg-3 col-sm-12 mr-4 mb-4" v-for="(crew, index) in crews" :key="index">
                                             <div style="color: white">{{ crew.name }}</div>
                                           <div style="color: #ffd80e">{{ crew.job }}</div>
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
    <!-- end details content -->
</section>

	<div class="container">
		<div class="row">
			<div class="col-12 mb-4">
				<h2 class="content__title">Casts</h2>
			</div>

			<div class="container">
                <div class="row">
                    <!-- card -->
                    <div class="col-6 col-sm-4 col-md-3 col-xl-2" v-for="(cast, index) in casts" :key="index">
                        <div class="card">
                            <div class="card__cover">
                             <NuxtLink
                                        :to="`/actor/${cast.id}`"
                                      >
                                    <img :src="`https://image.tmdb.org/t/p/w500/${cast.profile_path}`" alt="actor">
                             </NuxtLink>
                            </div>
                            <div class="card__content">
                                <h3 class="card__title">
                                   <NuxtLink
                                        :to="`/actor/${cast.id}`"
                                      >
                                     {{ cast.name }}

                                   </NuxtLink>
                                   </h3>

                                <span class="card__category" style="color: #ffd80e">
                                    {{ cast.character }}
                                </span>
                            </div>
                        </div>
                    </div>

                    <!-- end card -->
                </div>
            </div>
		</div>
	</div>
  	<div class="container">
		<div class="row">
			<div class="col-12 mb-4">
				<h2 class="content__title">Images</h2>
			</div>
			<!-- project gallery -->
				<div class="container">
                <div class="gallery" itemscope="">
                    <div class="row">
                        <!-- gallery item -->
                        <figure class="col-12 col-sm-6 col-xl-4" itemprop="associatedMedia" itemscope="" v-for="(image, index) in images" :key="index">
                            <a href="" itemprop="contentUrl" data-size="1920x1280">
                                <img :src="`https://image.tmdb.org/t/p/w500/${image.file_path}`" itemprop="thumbnail" alt="Image">
                            </a>
                        </figure>
                        <!-- end gallery item -->
                    </div>
                </div>
            </div>
			<!-- end project gallery -->
		</div>
	</div>
</div>
</div>
</template>

<script>
import axios from 'axios'
export default {
 name: 'singleTv',
  layout: 'CustomLayout',

  data() {
    return {
      tv: null,
      genres: [],
      casts: [],
      crews: [],
      images: [],
    }
  },

   async fetch() {
    await this.getSingleTv()
    await this.getCastsAndCrew()
    await this.getImages()
  },

 fetchDelay: 2000,

  methods: {
      async getSingleTv() {
      const data = axios.get(
        `https://api.themoviedb.org/3/tv/${this.$route.params.tvid}?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US`
      )
      const result = await data
      this.tv = result.data
      this.getGenres(result.data.genres)
    },

    getGenres(array){
      array.forEach(genre => {
        this.genres.push(genre.name)
      })
    },

    async getCastsAndCrew() {
      const data = axios.get(
        `https://api.themoviedb.org/3/tv/${this.$route.params.tvid}/credits?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US`
      )
      const result = await data
      let crews = result.data.crew.slice(0,3)
      let casts = result.data.cast.slice(0,6)
      casts.forEach((cast) => {
        this.casts.push(cast)
      })

      crews.forEach((crew) => {
        this.crews.push(crew)
      })
    },

    async getImages() {
       const data = axios.get(
        `https://api.themoviedb.org/3/tv/${this.$route.params.movieid}/images?api_key=5f41b1d865a3f2f545a6e714e41360fb&language=en-US`
      )
      const result = await data
      this.images = result.data.backdrops
    }
  }
}
</script>
