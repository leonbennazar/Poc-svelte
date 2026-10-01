<script lang="ts">
	let {
		onNavigate
	}: {
		onNavigate?: (destino: 'Storyline' | 'Titans') => void;
	} = $props();

	const tarjetas = [
		{
			clase: 'progress',
			titulo: 'Storyline',
			texto: 'See and mark key moments',
			detalle: '13 episodios clave del viaje de Eren'
		},
		{
			clase: 'titans',
			titulo: 'Titans',
			texto: 'Learn about different titans and their qualities',
			detalle: 'Habilidades, altura y lealtad de cada titán'
		}
	];
</script>

<div class="container">
	<div class="hero">
		<span class="eyebrow">Poc Svelte · Attack on Titan</span>
		<h1>Welcome</h1>
		<div class="rule"></div>
		<h2>Explore the world of Titans and key moments</h2>
	</div>

	<div class="boxes">
		{#each tarjetas as card (card.clase)}
			<button
				class="card {card.clase}"
				onclick={() => onNavigate?.(card.clase === 'progress' ? 'Storyline' : 'Titans')}
			>
				<span class="badge">{card.clase === 'progress' ? '01' : '02'}</span>
				<h3>{card.texto}</h3>
				<p>{card.detalle}</p>
				<span class="cta">Explore →</span>
			</button>
		{/each}
	</div>
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 40px 20px;
	}

	.hero {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
	}

	.eyebrow {
		font-size: 13px;
		letter-spacing: 4px;
		text-transform: uppercase;
		color: var(--red);
		font-weight: 700;
	}

	.hero h1 {
		margin: 12px 0 0;
		font-family: var(--font-display);
		font-size: clamp(56px, 12vw, 120px);
		letter-spacing: 4px;
		text-transform: uppercase;
		color: #fff;
		transition: color 1s ease;
	}

	.hero h1:hover {
		color: var(--red);
	}

	.rule {
		width: 140px;
		height: 4px;
		margin: 18px 0;
		border-radius: 4px;
		background: linear-gradient(90deg, transparent, var(--red), transparent);
		box-shadow: 0 0 12px rgba(229, 57, 53, 0.7);
	}

	.hero h2 {
		margin: 0;
		max-width: 640px;
		font-size: clamp(16px, 2.5vw, 22px);
		font-weight: 500;
		color: var(--text);
	}

	.boxes {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		gap: 40px;
		margin-top: 56px;
	}

	.card {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		gap: 10px;
		width: 300px;
		padding: 26px 24px;
		text-align: left;
		border-radius: 14px;
		border: 1px solid var(--line);
		border-top: 3px solid var(--red);
		background: var(--panel);
		backdrop-filter: blur(6px);
		color: var(--text);
		box-shadow: 0 6px 18px rgba(0, 0, 0, 0.45);
		transition:
			transform 0.2s ease,
			box-shadow 0.3s ease,
			border-color 0.3s ease;
		cursor: pointer;
	}

	.card:hover {
		transform: translateY(-6px);
		border-color: rgba(229, 57, 53, 0.65);
		box-shadow: 0 14px 30px rgba(213, 0, 0, 0.35);
	}

	.card:active {
		transform: scale(0.97);
		box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
	}

	.card:focus-visible {
		outline: 2px solid var(--red);
		outline-offset: 3px;
	}

	.badge {
		font-family: var(--font-display);
		font-size: 13px;
		font-weight: 700;
		letter-spacing: 2px;
		color: #fff;
		background: var(--red-dark);
		border-radius: 6px;
		padding: 4px 10px;
	}

	.card h3 {
		margin: 4px 0 0;
		font-size: 19px;
		line-height: 1.35;
		color: #fff;
	}

	.card p {
		margin: 0;
		font-size: 14px;
		line-height: 1.5;
		color: var(--text-dim);
	}

	.cta {
		margin-top: auto;
		font-size: 13px;
		font-weight: 700;
		letter-spacing: 2px;
		text-transform: uppercase;
		color: var(--red);
	}

	@media (max-width: 480px) {
		.boxes {
			gap: 24px;
			margin-top: 36px;
		}

		.card {
			width: 100%;
			max-width: 340px;
		}
	}
</style>
