<script lang="ts">
	import favicon from '$lib/assets/favicon.png';

	let { children } = $props();
</script>


<svelte:head>
	<link rel="icon" href={favicon} />
	<title>Attack on Titan</title>
</svelte:head>

{@render children?.()}
