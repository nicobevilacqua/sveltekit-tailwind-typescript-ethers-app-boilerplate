<script>
	import { page } from '$app/stores';

	import ConnectButton from '$lib/ConnectButton.svelte';
	import SwitchNetworkButton from '$lib/SwitchNetworkButton.svelte';
</script>

<header
	class="header text-center py-3 md:py-4 px-3 md:px-3 shadow-md border flex w-full bg-gradient-to-b from-white to-gray-100"
>
	<div class="container flex flex-wrap md:flex-row justify-between mx-auto">
		<div class="order-1 basis-3/12 md:basis-auto md:w-1/3 px-1">
			<SwitchNetworkButton />
		</div>

		<nav class="order-3 md:order-2 pt-2 md:pt-0 basis-full md:basis-auto" data-sveltekit-prefetch>
			<ul class="flex flex-row w-full items-center justify-center">
				<li
					class="p-2 hover:font-bold hover:underline"
					class:underline={$page.url.pathname === '/'}
				>
					<a href="/">Dashboard</a>
				</li>
				<li
					class="p-2 hover:font-bold hover:underline"
					class:underline={$page.url.pathname === '/borrow'}
				>
					<a href="/borrow">Borrow</a>
				</li>

				<li
					class="p-2 hover:font-bold hover:underline"
					class:underline={$page.url.pathname === '/lend'}
				>
					<a href="/lend">Lend</a>
				</li>
			</ul>
		</nav>

		<div
			class="order-2 md:order-3 flex justify-end shrink md:shrink-auto basis-9/12 md:basis-auto md:w-1/3 px-1"
		>
			<ConnectButton />
		</div>
	</div>
</header>
