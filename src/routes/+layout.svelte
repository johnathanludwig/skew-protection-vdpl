<script lang="ts">
    import { updated } from '$app/state';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();

	let toast = $state()
	$effect(() => {
		if (updated.current) {
			toast= 'A new update is available.'
		}
	});

	function onvisibilitychange() {
		if (document.visibilityState === 'visible') {
			updated.check();
		}
	}
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<svelte:document {onvisibilitychange} />

{@render children()}

{#if toast}
	<div class="">
		{toast}
		<button onclick={() => location.reload()}>Refresh</button>
	</div>
{/if}
