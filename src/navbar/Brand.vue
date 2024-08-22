<template>
	<div class="navbar-brand is-hidden-mobile" style="margin:0 15px">
		<div class="navbar-item">
			<slot>
				<router-link v-if="routeInstalled" :to="brand.path" class="store-link" exact>
					<img v-if="!loading" :src="brand.logo" :alt="brand.name" :class="isSafari?'w-auto':'w-100'" :style="{maxHeight: brand.size}" />
				</router-link>
				<a v-else :href="brand.path" class="store-link">
					<img v-if="brand.logo && !loading" :src="brand.logo" :alt="brand.name" :class="isSafari?'w-auto':'w-100'" :style="{maxHeight: brand.size}" />
				</a>
			</slot>
		</div>
	</div>
</template>
<script>
	export default {
		name: 'Brand',
		props: ["brand"],
		data() {
			return {
				loading: true,
				 isSafari: false
			}
		},
		mounted() {
			setTimeout(() => {
				this.loading = false;
			}, 1000)
		        this.isSafari = /^((?!chrome|android).)*safari/i.test(navigator.userAgent);

		},
		computed: {
			routeInstalled() {
				return this.$route
			}
		}
	}
</script>
<style scoped>
	.w-100 { width: 100%; }
        .w-auto { width: auto; }
</style>
