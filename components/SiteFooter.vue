<template>
<footer class="footer">
	<div class="container">
		<div class="row">
			<div class="col-12">
				<div class="footer__content">
              <NuxtLink to="/"  class="footer__logo">
            	<img src="../assets/img/logo.png" alt="" style="width: 50%">
               </NuxtLink>


					<span class="footer__copyright">© 2022 NerdFlix<br> Developed by <a href="https://joshuapaul.herokuapp.com" target="_blank">Joshua Paul</a></span>

					<button class="footer__back" type="button">
						<i class="icon ion-ios-arrow-round-up"></i>
					</button>
				</div>
			</div>
		</div>
	</div>
</footer>
</template>

<script>
export default {
name: 'siteFooter',
}
</script>
