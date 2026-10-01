<script lang="ts">
	import favicon from '$lib/assets/favicon.png';
	import '../app.css';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title>Attack on Svelte</title>
</svelte:head>

{@render children?.()}
