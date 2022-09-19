<script lang="ts">
	import { onMount } from 'svelte';

	import '../app.postcss';

	import Header from '$lib/Header.svelte';
	import Footer from '$lib/Footer.svelte';
	import Notification from '$lib/Notification.svelte';

	import { init } from '$store/wallet';

	onMount(() => {
		init();
	});
</script>

<Header />

<main class="content flex-1 text-sm flex justify-center">
	<slot />
</main>

<Footer />

<Notification />
