<script>
	let tab = $state('Home'); //dandole este valor inicial, siempre vamos a ir a la pagina storyline al recargar
	const paginas = ['Home', 'Storyline', 'Titans']; //lista

	import Progressbar from '$lib/components/progressbar.svelte';
	import Titans from '$lib/components/titans.svelte';
	import Home from '$lib/components/home.svelte';
</script>

<header class="header">
	<h1>Attack on Svelte</h1>
	<!--<p>Poc Svelte - Progress bar & character info</p>-->
</header>

<nav class="navbar">
	{#each paginas as p (p)}
		<!--recorre el array paginas y genera un boton por cada elemento.-->
		<button class:p-active={tab === p} onclick={() => (tab = p)}>
			<!--aplica la clase p-active solo si el botón corresponde al estado actual-->
			{p}
			<!--Este es el texto del boton, osea la varialbe p actual-->
		</button>
	{/each}
</nav>

<div class="content">
	{#if tab === 'Home'}
		<Home onNavigate={(destino) => (tab = destino)}></Home>
	{:else if tab === 'Storyline'}
		<Progressbar></Progressbar>
	{:else if tab === 'Titans'}
		<Titans></Titans>
	{/if}
</div>

<style>
	.header {
		position: fixed;
		z-index: 20;
		top: 0;
		left: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		height: 56px;
		width: 100%;
		color: #fff;
		background: var(--red);
		box-shadow: 0 2px 10px rgba(0, 0, 0, 0.55);
		border-bottom: 1px solid rgba(0, 0, 0, 0.35);
	}

	.header h1 {
		margin: 0;
		font-family: var(--font-display);
		font-size: 26px;
		letter-spacing: 3px;
		text-transform: uppercase;
	}

	.navbar {
		position: fixed;
		z-index: 20;
		top: 56px;
		left: 0;
		display: flex;
		width: 100%;
		background: var(--red);
		box-shadow: 0 4px 12px rgba(0, 0, 0, 0.45);
	}

	.navbar button {
		position: relative;
		flex: 1;
		font-size: 17px;
		font-weight: 600;
		letter-spacing: 1.5px;
		text-transform: uppercase;
		padding: 12px 10px;
		border: none;
		background: transparent;
		color: rgba(255, 255, 255, 0.85);
		transition:
			background 0.25s ease,
			color 0.25s ease;
	}

	.navbar button::after {
		content: '';
		position: absolute;
		left: 50%;
		bottom: 0;
		width: 0;
		height: 3px;
		background: #fff;
		border-radius: 3px 3px 0 0;
		transform: translateX(-50%);
		transition: width 0.25s ease;
	}

	.navbar button:hover {
		background: var(--red-dark);
		color: #fff;
		cursor: pointer;
	}

	.navbar button:focus-visible {
		outline: 2px solid #fff;
		outline-offset: -4px;
	}

	.navbar button.p-active {
		background: var(--red-dark);
		color: #fff;
	}

	.navbar button.p-active::after {
		width: 60%;
	}

	.content {
		margin-top: 100px; /**Hace que no quede arrbiba del todo el div*/
		min-height: calc(100vh - 100px);
		padding-bottom: 60px;
	}
</style>
