<template>
<header class="header">
		<div class="container">
			<div class="row">
				<div class="col-12">
					<div class="header__content">
						<!-- header logo -->
                     <NuxtLink to="/"  class="header__logo">
                     	<img src="../assets/img/logo.png" alt="" style="width: 50%">
                     </NuxtLink>
						<!-- end header logo -->

						<!-- header nav -->
						<ul class="header__nav">

							<li class="header__nav-item">
                 <NuxtLink to="/"  class="header__nav-link">Movies </NuxtLink>
							</li>
							<li class="header__nav-item">
                <NuxtLink to="/tvs"  class="header__nav-link">TV Shows </NuxtLink>
							</li>

							<li class="header__nav-item">
                <NuxtLink to="/actors"  class="header__nav-link">Actors </NuxtLink>
							</li>

						</ul>
						<!-- end header nav -->

						<!-- header auth -->
						<div class="header__auth">
                <SearchDropdown />

								<button class="header__search-button">
									<i class="icon ion-ios-search"></i>
								</button>
								<button class="header__search-close">
									<i class="icon ion-md-close"></i>
								</button>

							<button class="header__search-btn">
								<i class="icon ion-ios-search"></i>
							</button>

						</div>
						<!-- end header auth -->

						<!-- header menu btn -->
						<button class="header__btn" type="button">
							<span></span>
							<span></span>
							<span></span>
						</button>
						<!-- end header menu btn -->
					</div>
				</div>
			</div>
		</div>
	</header>
</template>

<script>

export default {
name: 'siteHeader',
}
</script>
