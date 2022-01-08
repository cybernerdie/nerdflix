<template>
	<section class="home">
		<div class="container">
			<div class="row">
				<div class="col-12 mb-4">
				<h2 class="content__title" style="color: #ffd80e">Popular Actors</h2>
				</div>

						<div class="container">
                    <div class="row">
                        <!-- actor card -->
                        <div class="col-6 col-sm-4 col-md-3 col-xl-2" v-for="(actor, index) in actors" :key="index">
                            <div class="card">
                                <div class="card__cover">
                                    <a href="">
                                        <img :src="`https://www.themoviedb.org/t/p/w470_and_h470_face/${actor.profile_path}`" alt="poster">
                                    </a>
                                </div>
                                <div class="card__content">
                                    <h3 class="card__title"><a href="">{{ actor.name }}</a></h3>
                                    <span class="card__category" style="color: #ffd80e">
                                        <!-- {{ $actor['known_for'] }} -->
                                    </span>
                                </div>
                            </div>
                        </div>
                        <!-- end actor card -->
                    </div>
                      <!-- <div style=" justify-content: space-between;">
                @if ($previous)
                    <a href="/actors/page/{{ $previous }}" style="color: white">Previous</a>
                @else
                    <div></div>
                @endif

                @if ($next)
                    <a href="/actors/page/{{ $next }}" style="color: white">Next</a>
                @else
                    <div></div>
                @endif

            </div> -->
                </div>
            </div>
		</div>
	</section>
</template>

<script>
export default {
  name: 'ActorCard',
    props: ['actors'],
}
</script>
