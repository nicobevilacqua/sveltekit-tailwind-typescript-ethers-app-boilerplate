<script type="ts">
	import { address, connect, onExpectedNetwork } from '$store/wallet';
	import {showNotification, NotificationType } from '$store/notifications';

	import Spinner from '$lib/Spinner.svelte';

	let loading = false;
	async function onConnect() {
		loading = true;
		try {
			await connect();
		} catch(error: any) {
			showNotification(error.message, {
				type: NotificationType.Error
			});
		}
		loading = false;
	}

	$: legend = loading ? 'Connecting' : $address ? $address : 'Conect Wallet';
</script>

{#if $onExpectedNetwork}
	<button
		on:click={onConnect}
		disabled={loading || !$onExpectedNetwork}
		class="
			button
		bg-green-500
		hover:bg-green-600
			hover:underline
			hover:shadow-md
		disabled:bg-gray-500
		text-white
			px-4
			py-2
			rounded
			transition
			easy-in-out
			duration-150
			flex
			flex-row
			items-center
			justify-center
			text-sm
			w-full
			md:w-auto
			my-1 
			md:my-0
			cursor-default
		"
		class:cursor-pointer={!$address}
	>
		{#if loading}
			<div class="pr-2">
				<Spinner />
			</div>
		{/if}

		<span
			class="overflow-ellipsis overflow-hidden w-24 md:w-32 lg:w-auto max-w-xs
	">{legend}</span
		>
	</button>
{/if}
