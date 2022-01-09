<template>
	   <div class="container">
            <div class="row movie">
		<!-- movie card -->
					<div class="col-6 col-sm-4 col-md-3 col-xl-2 movie" v-for="(movie, index) in movies" :key="index">
						<div class="card">
							<div class="card__cover">
								<img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="">
                   <NuxtLink
              class="card__play"
               :to="`/movies/${movie.id}`"
            >
            <i class="icon ion-ios-play"></i>
            </NuxtLink>
								<span class="card__rate card__rate--green">{{ movie.vote_average * 10}}%</span>
							</div>
							<div class="card__content">
								<h3 class="card__title">
                   <NuxtLink
                   :to="`/movies/${movie.id}`"
            >
            {{ movie.title.slice(0, 25)}}
            </NuxtLink>
                  </h3>
							<span class="card__category" style="color: #ffd80e">
								{{ movie.genres.join(', ') }}
								</span>
							</div>
						</div>
					</div>
					<!-- end movie card -->
              </div>
           </div>
</template>

<script>
export default {
  name: 'MovieCard',
    props: ['movies'],
}
</script>
