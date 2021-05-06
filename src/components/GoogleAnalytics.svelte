<script>
	// https://tute.io/google-analytics-svelte-sapper
	import { stores } from "@sapper/app";
	const { page, session } = stores();

	$: {
		/* eslint-disable no-undef */
		if (typeof gtag !== "undefined") {
			gtag("config", "G-TEDZ0RF35G", {
				page_path: $page.path,
			});
		}
	}
</script>
