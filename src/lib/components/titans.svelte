<script lang="ts">
	import { onMount } from 'svelte';

	type Titan = {
		id: number;
		name: string;
		abilities: string;
		height: string | number;
		allegiance: string;
	};

	let data = $state<Titan[]>([]);
	let cargando = $state(true);
	let error = $state<string | null>(null);
	let mostrar = $state<number | null>(null);

	async function getTitans() {
		cargando = true;
		error = null;
		try {
			const req = await fetch('https://api.attackontitanapi.com/titans/');
			if (!req.ok) throw new Error(`HTTP ${req.status}`);
			const res = await req.json();
			data = res.results ?? [];
			if (data.length === 0) throw new Error('empty');
		} catch {
			error = 'We could not reach the Titans API.';
			data = [];
		} finally {
			cargando = false;
		}
	}

	onMount(() => {
		getTitans();
	});

	function cerrar() {
		mostrar = null;
	}
</script>

<svelte:window
	onkeydown={(e) => {
		if (e.key === 'Escape') cerrar();
	}}
/>

<section class="titans">
	<div class="head">
		<span class="eyebrow">Titans</span>
		<h2>Every Titan, its abilities and allegiance</h2>
		{#if !cargando && !error}
			<span class="count">{data.length} registered</span>
		{/if}
	</div>

	{#if cargando}
		<div class="grid">
			{#each Array.from({ length: 8 }, (_, i) => i) as n (n)}
				<div class="card skeleton">
					<div class="ph"></div>
					<div class="bar"></div>
				</div>
			{/each}
		</div>
		<p class="estado">Loading titans…</p>
	{:else if error}
		<div class="error">
			<p>{error}</p>
			<button onclick={getTitans}>Retry</button>
		</div>
	{:else}
		<div class="grid">
			{#each data as titan (titan.id)}
				<button class="card" onclick={() => (mostrar = titan.id)}>
					<span class="img-wrap">
						<img src="/titans/{titan.id}.png" alt={titan.name} loading="lazy" />
					</span>
					<span class="descripcion">{titan.name}</span>
				</button>
			{/each}
		</div>
	{/if}
</section>

{#each data as titan (titan.id)}
	{#if mostrar === titan.id}
		<div class="overlay">
			<button class="backdrop" aria-label="Close" onclick={cerrar}></button>
			<div class="popup" role="dialog" aria-modal="true" aria-label={titan.name}>
				<header>
					<h1>{titan.name}</h1>
					<button class="close" aria-label="Close" onclick={cerrar}>×</button>
				</header>
				<div class="body">
					<img src="/titans/{titan.id}.png" alt={titan.name} />
					<dl>
						<div>
							<dt>Abilities</dt>
							<dd>{titan.abilities}</dd>
						</div>
						<div>
							<dt>Height</dt>
							<dd>{titan.height} m</dd>
						</div>
						<div>
							<dt>Allegiance</dt>
							<dd>{titan.allegiance}</dd>
						</div>
					</dl>
				</div>
				<footer>
					<button class="btn-close" onclick={cerrar}>Close</button>
				</footer>
			</div>
		</div>
	{/if}
{/each}

<style>
	.titans {
		padding: 20px clamp(12px, 4vw, 40px) 0;
	}

	.head {
		position: relative;
		max-width: 1100px;
		margin: 0 auto;
		padding: 24px clamp(16px, 3vw, 32px);
		border-radius: 14px;
		border: 1px solid var(--line);
		border-left: 4px solid var(--red);
		background: var(--panel);
		box-shadow: 0 6px 18px rgba(0, 0, 0, 0.45);
	}

	.eyebrow {
		font-size: 12px;
		font-weight: 700;
		letter-spacing: 3px;
		text-transform: uppercase;
		color: var(--red);
	}

	.head h2 {
		margin: 6px 0 0;
		font-size: clamp(18px, 3vw, 26px);
		color: #fff;
	}

	.count {
		position: absolute;
		right: clamp(16px, 3vw, 32px);
		bottom: 26px;
		font-size: 13px;
		letter-spacing: 1px;
		color: var(--text-dim);
	}

	.grid {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
		gap: 28px;
		max-width: 1200px;
		margin: 0 auto;
		padding: 40px 0 20px;
	}

	.card {
		display: flex;
		flex-direction: column;
		padding: 0;
		overflow: hidden;
		text-align: center;
		border-radius: 12px;
		border: 1px solid var(--line);
		background: var(--panel);
		color: var(--text);
		cursor: pointer;
		box-shadow: 0 6px 16px rgba(0, 0, 0, 0.45);
		transition:
			transform 0.2s ease,
			box-shadow 0.25s ease,
			border-color 0.25s ease;
	}

	.card:hover {
		transform: translateY(-6px);
		border-color: rgba(229, 57, 53, 0.7);
		box-shadow: 0 14px 30px rgba(213, 0, 0, 0.35);
	}

	.card:focus-visible {
		outline: 2px solid var(--red);
		outline-offset: 3px;
	}

	.img-wrap {
		display: block;
		overflow: hidden;
		background: #000;
	}

	.card img {
		display: block;
		width: 100%;
		aspect-ratio: 3 / 4;
		object-fit: cover;
		transition:
			transform 0.3s ease,
			filter 0.3s ease;
		filter: saturate(0.9) brightness(0.92);
	}

	.card:hover img {
		transform: scale(1.06);
		filter: none;
	}

	.descripcion {
		display: block;
		padding: 12px 10px;
		font-size: 15px;
		font-weight: 700;
		letter-spacing: 0.5px;
		color: #fff;
		background: linear-gradient(180deg, var(--red), var(--red-dark));
		border-top: 1px solid rgba(255, 255, 255, 0.15);
	}

	.skeleton {
		cursor: default;
	}

	.skeleton:hover {
		transform: none;
		border-color: var(--line);
		box-shadow: 0 6px 16px rgba(0, 0, 0, 0.45);
	}

	.ph {
		width: 100%;
		aspect-ratio: 3 / 4;
		background: linear-gradient(100deg, #1b1b20 30%, #2b2b32 50%, #1b1b20 70%);
		background-size: 200% 100%;
		animation: shimmer 1.4s infinite linear;
	}

	.bar {
		height: 44px;
		background: linear-gradient(100deg, #3a1212 30%, #582020 50%, #3a1212 70%);
		background-size: 200% 100%;
		animation: shimmer 1.4s infinite linear;
	}

	@keyframes shimmer {
		to {
			background-position: -200% 0;
		}
	}

	.estado {
		text-align: center;
		color: var(--text-dim);
		letter-spacing: 1px;
	}

	.error {
		max-width: 480px;
		margin: 60px auto;
		padding: 32px;
		text-align: center;
		border-radius: 14px;
		border: 1px solid rgba(229, 57, 53, 0.5);
		background: var(--panel);
	}

	.error p {
		margin: 0 0 18px;
		color: var(--text);
	}

	.error button,
	.btn-close,
	.close {
		font-weight: 700;
		letter-spacing: 1px;
		color: #fff;
		background: linear-gradient(180deg, var(--red), var(--red-dark));
		border: none;
		border-radius: 8px;
		cursor: pointer;
		transition:
			filter 0.2s ease,
			transform 0.15s ease;
	}

	.error button {
		padding: 10px 24px;
	}

	.error button:hover,
	.btn-close:hover,
	.close:hover {
		filter: brightness(1.15);
	}

	.error button:active,
	.btn-close:active,
	.close:active {
		transform: scale(0.96);
	}

	.overlay {
		position: fixed;
		inset: 0;
		z-index: 50;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 16px;
	}

	.backdrop {
		position: absolute;
		inset: 0;
		padding: 0;
		border: none;
		background: rgba(8, 8, 12, 0.8);
		backdrop-filter: blur(4px);
		cursor: pointer;
	}

	.popup {
		position: relative;
		width: min(520px, 100%);
		max-height: 90vh;
		overflow-y: auto;
		border-radius: 16px;
		border: 1px solid rgba(229, 57, 53, 0.45);
		background: var(--panel-solid);
		box-shadow: 0 24px 60px rgba(0, 0, 0, 0.75);
		animation: pop 0.25s ease;
	}

	@keyframes pop {
		from {
			opacity: 0;
			transform: translateY(14px) scale(0.97);
		}
	}

	.popup header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 12px;
		padding: 16px 18px;
		background: linear-gradient(90deg, var(--red-deep), var(--red-dark));
	}

	.popup h1 {
		margin: 0;
		font-family: var(--font-display);
		font-size: clamp(20px, 5vw, 28px);
		letter-spacing: 1px;
		color: #fff;
	}

	.close {
		flex-shrink: 0;
		width: 36px;
		height: 36px;
		font-size: 22px;
		line-height: 1;
		border-radius: 50%;
		background: rgba(0, 0, 0, 0.35);
	}

	.body {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 18px;
		padding: 22px;
	}

	.body > img {
		width: min(260px, 70%);
		aspect-ratio: 3 / 4;
		object-fit: cover;
		border-radius: 12px;
		border: 2px solid rgba(255, 255, 255, 0.18);
		box-shadow: 0 10px 24px rgba(0, 0, 0, 0.6);
	}

	dl {
		display: grid;
		gap: 10px;
		width: 100%;
		margin: 0;
	}

	dl div {
		display: flex;
		flex-wrap: wrap;
		gap: 4px 10px;
		padding: 10px 14px;
		border-radius: 10px;
		background: rgba(255, 255, 255, 0.05);
		border-left: 3px solid var(--red);
	}

	dt {
		width: 100%;
		font-size: 11px;
		font-weight: 700;
		letter-spacing: 2px;
		text-transform: uppercase;
		color: var(--red);
	}

	dd {
		margin: 0;
		font-size: 15px;
		color: var(--text);
	}

	footer {
		display: flex;
		justify-content: center;
		padding: 0 22px 22px;
	}

	.btn-close {
		padding: 10px 34px;
	}

	@media (max-width: 560px) {
		.count {
			position: static;
			display: inline-block;
			margin-top: 8px;
		}
	}
</style>
