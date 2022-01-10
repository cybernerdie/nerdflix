<template>
  <div class="container">
            <div class="row">
		<!-- tv card -->
					<div class="col-6 col-sm-4 col-md-3 col-xl-2" v-for="(tv, index) in tvs" :key="index">
						<div class="card">
							<div class="card__cover">
								<img :src="`https://image.tmdb.org/t/p/w500/${tv.poster_path}`" alt="">
                   <NuxtLink
              class="card__play"
               :to="`/tv/${tv.id}`"
            >
            <i class="icon ion-ios-play"></i>
            </NuxtLink>
								<span class="card__rate card__rate--green">{{ tv.vote_average * 10}}%</span>
							</div>
							<div class="card__content">
								<h3 class="card__title">
                  <NuxtLink
                   :to="`/tv/${tv.id}`"
            >
            {{ tv.name.slice(0, 25)}}
            </NuxtLink>
                  </h3>
								<span class="card__category" style="color: #ffd80e">
						{{ tv.genres.join(', ') }}
								</span>
							</div>
						</div>
					</div>
					<!-- end tv card -->
              </div>
           </div>
</template>

<script>
export default {
  name: 'TvCard',
    props: ['tvs'],
}
</script>
