<script lang="ts">
	let events = $state([
		{ checked: false, img: '/shing-attack.webp', titulo: 'Shingeki no Kyojin' },
		{ checked: false, img: '/titan-mama-eren.jpg', titulo: 'The Day It All Began' },
		{ checked: false, img: '/eren-tropas.jpg', titulo: 'Eren Joins the Troops' },
		{ checked: false, img: '/eren-chico.jpg', titulo: 'Eren as a Child' },
		{ checked: false, img: '/eren-cubre-muro.jpg', titulo: 'Covering the Wall' },
		{ checked: false, img: '/titan-hembra.jpg', titulo: 'The Female Titan' },
		{ checked: false, img: '/traitors.png', titulo: 'Traitors' },
		{ checked: false, img: '/erwin.jpg', titulo: 'Commander Erwin' },
		{ checked: false, img: '/eren-mikasa-armin.jpg', titulo: 'Eren, Mikasa & Armin' },
		{ checked: false, img: '/grisha.jpg', titulo: 'Grisha Yeager' },
		{ checked: false, img: '/eren-historia.jpg', titulo: 'Eren & Historia' },
		{ checked: false, img: '/eren-grande.jpg', titulo: "Eren's Attack Titan" },
		{ checked: false, img: '/ult-foto.jpg', titulo: 'The Last Photo' }
	]);

	let completas = $derived(events.filter((e) => e.checked).length);
	let progreso = $derived((completas / events.length) * 100);
</script>

<section class="storyline">
	<div class="head">
		<div class="head-text">
			<span class="eyebrow">Storyline</span>
			<h2>Mark every key moment of the series</h2>
		</div>
		<div class="stats">
			<span class="pct">{Math.round(progreso)}%</span>
			<span class="count">{completas} / {events.length} events</span>
		</div>
	</div>

	<div class="skeleton">
		<div class="fill" style="width: {progreso}%"></div>
		{#if progreso === 100}
			<img
				src="/erenfounder.jpg"
				alt="eren"
				class="runner"
				style="left: clamp(30px, {progreso}%, calc(100% - 30px))"
			/>
		{:else}
			<img
				src="/eren.png"
				alt="eren"
				class="runner"
				style="left: clamp(30px, {progreso}%, calc(100% - 30px))"
			/>
		{/if}
	</div>

	<div class="checkboxes">
		{#each events as e, i (e.titulo)}
			<label class="event" class:on={e.checked}>
				<input type="checkbox" bind:checked={e.checked} />
				<span class="frame">
					<img src={e.img} alt={e.titulo} />
					<span class="check" aria-hidden="true"></span>
					<span class="n">{String(i + 1).padStart(2, '0')}</span>
				</span>
				<span class="titulo">{e.titulo}</span>
			</label>
		{/each}
	</div>
</section>

<style>
	.storyline {
		padding: 20px clamp(12px, 4vw, 40px) 0;
	}

	.head {
		display: flex;
		flex-wrap: wrap;
		align-items: flex-end;
		justify-content: space-between;
		gap: 16px;
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

	.stats {
		display: flex;
		flex-direction: column;
		align-items: flex-end;
		gap: 2px;
	}

	.pct {
		font-family: var(--font-display);
		font-size: clamp(28px, 5vw, 40px);
		font-weight: 700;
		line-height: 1;
		color: #fff;
	}

	.count {
		font-size: 13px;
		letter-spacing: 1px;
		color: var(--text-dim);
	}

	.skeleton {
		position: relative;
		max-width: 1100px;
		height: 36px;
		margin: 60px auto 0;
		border-radius: 20px;
		background: #2a2a30;
		box-shadow:
			inset 0 2px 6px rgba(0, 0, 0, 0.7),
			0 2px 8px rgba(0, 0, 0, 0.4);
		border: 1px solid var(--line);
	}

	.fill {
		height: 100%;
		border-radius: 20px;
		background: linear-gradient(90deg, #1b5e20, #43a047 60%, #66bb6a);
		box-shadow: 0 0 16px rgba(102, 187, 106, 0.55);
		transition: width 0.4s ease;
	}

	.runner {
		position: absolute;
		top: -54px;
		height: 58px;
		transform: translateX(-50%);
		filter: drop-shadow(0 4px 6px rgba(0, 0, 0, 0.7));
		transition: left 0.4s ease;
		pointer-events: none;
	}

	.checkboxes {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
		gap: 24px;
		max-width: 1200px;
		margin: 0 auto;
		padding: 60px 0 20px;
	}

	.event {
		display: flex;
		flex-direction: column;
		gap: 10px;
		padding: 12px;
		border-radius: 12px;
		border: 1px solid var(--line);
		background: var(--panel);
		cursor: pointer;
		transition:
			transform 0.2s ease,
			border-color 0.25s ease,
			box-shadow 0.25s ease;
	}

	.event:hover {
		transform: translateY(-4px);
		border-color: rgba(229, 57, 53, 0.6);
		box-shadow: 0 10px 22px rgba(0, 0, 0, 0.5);
	}

	.event input {
		position: absolute;
		width: 1px;
		height: 1px;
		opacity: 0;
		pointer-events: none;
	}

	.frame {
		position: relative;
		display: block;
		overflow: hidden;
		height: 110px;
		border-radius: 8px;
		border: 2px solid transparent;
		background: #000;
		transition: border-color 0.25s ease;
	}

	.frame img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		display: block;
		filter: grayscale(0.85) brightness(0.65);
		transition:
			filter 0.3s ease,
			transform 0.3s ease;
	}

	.event:hover .frame img {
		transform: scale(1.05);
	}

	.event input:focus-visible + .frame {
		outline: 2px solid var(--red);
		outline-offset: 2px;
	}

	.check {
		position: absolute;
		top: 8px;
		right: 8px;
		width: 24px;
		height: 24px;
		border-radius: 50%;
		background: rgba(0, 0, 0, 0.65);
		border: 2px solid rgba(255, 255, 255, 0.7);
		opacity: 0;
		transform: scale(0.5);
		transition:
			opacity 0.2s ease,
			transform 0.2s ease;
	}

	.check::after {
		content: '';
		position: absolute;
		top: 4px;
		left: 8px;
		width: 5px;
		height: 10px;
		border: solid #fff;
		border-width: 0 2.5px 2.5px 0;
		transform: rotate(45deg);
	}

	.n {
		position: absolute;
		left: 0;
		bottom: 0;
		padding: 2px 8px;
		font-family: var(--font-display);
		font-size: 12px;
		font-weight: 700;
		letter-spacing: 1px;
		color: #fff;
		background: rgba(0, 0, 0, 0.7);
		border-radius: 0 8px 0 8px;
	}

	.titulo {
		font-size: 13.5px;
		font-weight: 600;
		line-height: 1.35;
		color: var(--text-dim);
		transition: color 0.25s ease;
	}

	.event.on {
		border-color: rgba(102, 187, 106, 0.75);
		box-shadow: 0 0 0 1px rgba(102, 187, 106, 0.35);
	}

	.event.on .frame {
		border-color: #43a047;
	}

	.event.on .frame img {
		filter: none;
	}

	.event.on .check {
		opacity: 1;
		transform: scale(1);
	}

	.event.on .titulo {
		color: #fff;
	}

	@media (max-width: 560px) {
		.head {
			flex-direction: column;
			align-items: flex-start;
		}

		.stats {
			align-items: flex-start;
		}

		.skeleton {
			margin-top: 64px;
		}
	}
</style>
