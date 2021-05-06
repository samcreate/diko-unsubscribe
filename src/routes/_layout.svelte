<script>
	import Nav from "../components/Nav.svelte";
	import GoogleAnalytics from "../components/GoogleAnalytics.svelte";

	export let segment;
</script>

<main>
	<slot />
</main>
<GoogleAnalytics />

<style>
	main {
		width: 100vw;
		height: 100vh;
	}
	@media only screen and (max-width: 39.1875rem) {
		main {
			width: 100%;
			height: 100%;
			min-height: -webkit-fill-available;
		}
	}
</style>
