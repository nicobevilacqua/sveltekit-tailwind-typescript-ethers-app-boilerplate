<script type="ts">
	import { metamask, expectedNetwork, switchNetwork, onExpectedNetwork } from '$store/wallet';
	import { showNotification, NotificationType } from '$store/notifications';

	import Spinner from '$lib/Spinner.svelte';

	let loading = false;
	async function onSwitchNetwork() {
		loading = true;
		try {
			await switchNetwork();
		} catch (error: any) {
			showNotification(error.message, {
				type: NotificationType.Error, 
			})
		}
		loading = false;
	}

	$: legend = loading
		? 'Switching'
		: !$onExpectedNetwork
		? `Switch to ${$expectedNetwork.name}`
		: $expectedNetwork.name;
</script>

{#if $metamask}
	<button
		on:click={onSwitchNetwork}
		disabled={loading}
		class="
			button 
			bg-blue-500
		hover:bg-blue-600
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
			my-1 md:my-0
			cursor-default
		"
		class:cursor-pointer={!$onExpectedNetwork}
	>
		{#if loading}
			<div class="pr-2">
				<Spinner />
			</div>
		{/if}

		<span>{legend}</span></button
	>
{/if}
