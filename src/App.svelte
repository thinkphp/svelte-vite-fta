<script lang="ts">
	import Title from './Title.svelte';
	import Footer from './Footer.svelte';

	const pkg = {
		name: 'svelte',
		version: 5,
		speed: 'very',
		doit: 'thinkphp',
		website: 'https://svelte.dev'
	};

	let a = $state<number>(2);
	let factorization = $state('');
	let squareRoot = $state('');
	let primeStatus = $state('');
	let hasCalculated = $state(false);

	function isPrime(n: number): boolean {
		if (n < 2) return false;

		for (let i = 2; i <= Math.sqrt(n); i++) {
			if (n % i === 0) return false;
		}

		return true;
	}

	function factorize(n: number): string {
		const originalNumber = n;
		const factors: string[] = [];

		let i = 2;

		while (n !== 1) {
			let power = 0;

			while (n % i === 0) {
				power++;
				n = n / i;
			}

			if (power > 0) {
				factors.push(power === 1 ? `${i}` : `${i}^${power}`);
			}

			i++;
		}

		return `${originalNumber} = ${factors.join(' × ')}`;
	}

	function calculate(): void {
		hasCalculated = false;
		factorization = '';
		squareRoot = '';
		primeStatus = '';

		const n = Number(a);

		if (!Number.isInteger(n) || n < 1) {
			factorization = 'Please enter a positive integer.';
			return;
		}

		factorization = factorize(n);

		primeStatus = isPrime(n)
			? 'This number is prime.'
			: 'This number is composite.';

		squareRoot = Math.sqrt(n).toFixed(6);

		hasCalculated = true;
	}

	function handleKeydown(event: KeyboardEvent): void {
		if (event.key === 'Enter') {
			calculate();
		}
	}
</script>

<svelte:head>
	<title>Number Theory Calculator</title>
	<meta
		name="description"
		content="A modern number theory calculator built with Svelte 5"
	/>
</svelte:head>

<div class="page">
	<div class="background-orb orb-one"></div>
	<div class="background-orb orb-two"></div>

	<header class="topbar">
		<div class="brand">
			<div class="logo">∑</div>

			<div>
				<span class="brand-title">Number Theory</span>
				<span class="brand-subtitle">Svelte 5 Calculator</span>
			</div>
		</div>

		<div class="version">
			<span class="dot"></span>
			Svelte 5
		</div>
	</header>

	<main class="content">
		<section class="hero">
			<div class="badge">
				<span>✦</span>
				Interactive mathematics
			</div>

			<h1>

				<span>Fundamental Theorem of Arithmetic</span>
			</h1>

			<p class="hero-description">
				Explore prime factorization and square roots with a simple,
				interactive calculator.
			</p>
		</section>

		<section class="calculator-card">
			<div class="card-header">
				<div>
					<h2>Number calculator</h2>
					<p>Enter a positive integer to begin.</p>
				</div>

				<div class="number-icon">#</div>
			</div>

			<div class="input-group">
				<label for="number">Your number</label>

				<div class="input-wrapper">
					<span class="input-prefix">n =</span>

					<input
						id="number"
						type="number"
						min="1"
						step="1"
						bind:value={a}
						onkeydown={handleKeydown}
						placeholder="Enter a number..."
					/>
				</div>
			</div>

			<button class="calculate-button" onclick={calculate}>
				<span>Calculate</span>
				<span class="arrow">→</span>
			</button>

			<p class="hint">
				Press <kbd>Enter</kbd> to calculate
			</p>
		</section>

		{#if hasCalculated}
			<section class="results">
				<div class="results-title">
					<div>
						<span class="eyebrow">RESULTS</span>
						<h2>Analysis for {a}</h2>
					</div>

					<div class="success-icon">✓</div>
				</div>

				<div class="result-grid">
					<div class="result-card">
						<div class="result-label">
							<span class="result-icon">✦</span>
							Prime factorization
						</div>

						<div class="factorization">
							{factorization}
						</div>

						<p class="result-description">
							The unique representation of {a} as a product of
							prime numbers.
						</p>
					</div>

					<div class="result-card">
						<div class="result-label">
							<span class="result-icon">√</span>
							Square root
						</div>

						<div class="sqrt-value">
							<span>√{a}</span>
							<strong>{squareRoot}</strong>
						</div>

						<p class="result-description">
							Calculated using the square root function.
						</p>
					</div>

					<div class="result-card prime-card">
						<div class="result-label">
							<span class="result-icon">◆</span>
							Prime status
						</div>

						<div class:prime={primeStatus.includes('prime.') && !primeStatus.includes('composite')} class="status">
							{#if primeStatus.includes('prime.') && !primeStatus.includes('composite')}
								<span class="status-dot"></span>
								Prime number
							{:else}
								<span class="status-dot composite"></span>
								Composite number
							{/if}
						</div>

						<p class="result-description">
							{primeStatus}
						</p>
					</div>
				</div>
			</section>
		{/if}

		<section class="info">
			<div class="info-icon">i</div>

			<div>
				<h3>Fundamental theorem of arithmetic</h3>

				<p>
					Every integer greater than 1 is either a prime number or can
					be represented as a product of prime numbers. This
					representation is unique, apart from the order of the
					factors.
				</p>
			</div>
		</section>

		<Title
			name={pkg.name}
			version={pkg.version}
			speed={pkg.speed}
			website={pkg.website}
			doit={pkg.doit}
		/>

		<Footer />
	</main>
</div>

<style>
.results {
	margin-top: 20px;
}

.info {
	margin-top: 20px;
}

:global(.footer) {
	margin-top: 30px;
}
	.page {
		position: relative;
		min-height: 100vh;
		overflow: hidden;
		background:
			radial-gradient(circle at 50% -10%, #18233e 0, transparent 45%),
			#080b14;
		padding: 28px 20px 60px;
	}

	.background-orb {
		position: absolute;
		width: 500px;
		height: 500px;
		border-radius: 50%;
		filter: blur(100px);
		opacity: 0.12;
		pointer-events: none;
	}

	.orb-one {
		top: 20%;
		left: -300px;
		background: #6366f1;
	}

	.orb-two {
		right: -300px;
		top: 50%;
		background: #14b8a6;
	}

	.topbar {
		position: relative;
		z-index: 1;
		max-width: 1100px;
		margin: auto;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.brand {
		display: flex;
		align-items: center;
		gap: 12px;
	}

	.logo {
		width: 42px;
		height: 42px;
		display: grid;
		place-items: center;
		border-radius: 12px;
		background: linear-gradient(135deg, #6366f1, #8b5cf6);
		font-size: 22px;
		font-weight: 800;
		box-shadow: 0 8px 30px rgb(99 102 241 / 25%);
	}

	.brand-title,
	.brand-subtitle {
		display: block;
	}

	.brand-title {
		font-weight: 700;
		font-size: 15px;
	}

	.brand-subtitle {
		margin-top: 2px;
		color: #64748b;
		font-size: 12px;
	}

	.version {
		display: flex;
		align-items: center;
		gap: 7px;
		padding: 7px 12px;
		border: 1px solid #1e293b;
		border-radius: 999px;
		color: #94a3b8;
		font-size: 12px;
		background: rgb(15 23 42 / 60%);
	}

	.dot {
		width: 7px;
		height: 7px;
		border-radius: 50%;
		background: #22c55e;
		box-shadow: 0 0 10px rgb(34 197 94 / 70%);
	}

	.content {
		position: relative;
		z-index: 1;
		max-width: 900px;
		margin: auto;
	}

	.hero {
		text-align: center;
		padding: 90px 20px 45px;
	}

	.badge {
		display: inline-flex;
		align-items: center;
		gap: 7px;
		padding: 7px 13px;
		border: 1px solid #29334a;
		border-radius: 999px;
		background: rgb(15 23 42 / 70%);
		color: #a5b4fc;
		font-size: 12px;
		font-weight: 600;
	}

	.hero h1 {
		max-width: 750px;
		margin: 22px auto 16px;
		font-size: clamp(42px, 7vw, 70px);
		line-height: 1;
		letter-spacing: -3px;
	}

	.hero h1 span {
		display: block;
		background: linear-gradient(90deg, #a78bfa, #38bdf8);
		-webkit-background-clip: text;
		background-clip: text;
		color: transparent;
	}

	.hero-description {
		max-width: 580px;
		margin: auto;
		color: #94a3b8;
		font-size: 17px;
		line-height: 1.7;
	}

	.calculator-card,
	.results,
	.info {
		border: 1px solid #1e293b;
		border-radius: 24px;
		background: rgb(15 23 42 / 75%);
		box-shadow: 0 20px 70px rgb(0 0 0 / 25%);
		backdrop-filter: blur(20px);
	}

	.calculator-card {
		padding: 30px;
	}

	.card-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 30px;
	}

	.card-header h2 {
		margin: 0 0 6px;
		font-size: 21px;
	}

	.card-header p {
		margin: 0;
		color: #64748b;
		font-size: 14px;
	}

	.number-icon {
		width: 45px;
		height: 45px;
		display: grid;
		place-items: center;
		border-radius: 14px;
		background: #1e1b4b;
		color: #a5b4fc;
		font-size: 20px;
		font-weight: 700;
	}

	.input-group label {
		display: block;
		margin-bottom: 9px;
		color: #cbd5e1;
		font-size: 13px;
		font-weight: 600;
	}

	.input-wrapper {
		display: flex;
		align-items: center;
		border: 1px solid #334155;
		border-radius: 14px;
		background: #0b1120;
		transition: 0.2s;
	}

	.input-wrapper:focus-within {
		border-color: #818cf8;
		box-shadow: 0 0 0 4px rgb(99 102 241 / 12%);
	}

	.input-prefix {
		padding-left: 17px;
		color: #64748b;
		font-family: monospace;
	}

	input {
		width: 100%;
		padding: 16px;
		border: 0;
		outline: none;
		background: transparent;
		color: white;
		font-size: 17px;
	}

	input::placeholder {
		color: #475569;
	}

	.calculate-button {
		width: 100%;
		margin-top: 16px;
		padding: 15px 20px;
		border: 0;
		border-radius: 14px;
		background: linear-gradient(135deg, #6366f1, #8b5cf6);
		color: white;
		font-weight: 700;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 10px;
		transition:
			transform 0.2s,
			box-shadow 0.2s;
	}

	.calculate-button:hover {
		transform: translateY(-2px);
		box-shadow: 0 12px 30px rgb(99 102 241 / 30%);
	}

	.arrow {
		font-size: 20px;
	}

	.hint {
		margin: 12px 0 0;
		text-align: center;
		color: #475569;
		font-size: 12px;
	}

	kbd {
		padding: 2px 6px;
		border: 1px solid #334155;
		border-radius: 5px;
		color: #94a3b8;
	}

	.results {
		margin-top: 20px;
		padding: 30px;
	}

	.results-title {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 22px;
	}

	.eyebrow {
		color: #818cf8;
		font-size: 10px;
		font-weight: 800;
		letter-spacing: 2px;
	}

	.results-title h2 {
		margin: 5px 0 0;
		font-size: 22px;
	}

	.success-icon {
		width: 38px;
		height: 38px;
		display: grid;
		place-items: center;
		border-radius: 50%;
		background: rgb(34 197 94 / 12%);
		color: #4ade80;
	}

	.result-grid {
		display: grid;
		grid-template-columns: 1.5fr 1fr;
		gap: 14px;
	}

	.result-card {
		padding: 20px;
		border: 1px solid #1e293b;
		border-radius: 17px;
		background: rgb(2 6 23 / 45%);
	}

	.prime-card {
		grid-column: span 2;
	}

	.result-label {
		display: flex;
		align-items: center;
		gap: 8px;
		color: #94a3b8;
		font-size: 12px;
		font-weight: 600;
	}

	.result-icon {
		color: #a78bfa;
		font-size: 17px;
	}

	.factorization {
		margin-top: 17px;
		color: #f8fafc;
		font-family: monospace;
		font-size: 22px;
		font-weight: 700;
		overflow-wrap: anywhere;
	}

	.sqrt-value {
		display: flex;
		align-items: baseline;
		gap: 10px;
		margin-top: 17px;
	}

	.sqrt-value span {
		color: #94a3b8;
		font-size: 14px;
	}

	.sqrt-value strong {
		color: #38bdf8;
		font-size: 24px;
	}

	.result-description {
		margin: 12px 0 0;
		color: #64748b;
		font-size: 12px;
		line-height: 1.5;
	}

	.status {
		display: flex;
		align-items: center;
		gap: 9px;
		margin-top: 16px;
		color: #fbbf24;
		font-size: 19px;
		font-weight: 700;
	}

	.status.prime {
		color: #4ade80;
	}

	.status-dot {
		width: 9px;
		height: 9px;
		border-radius: 50%;
		background: #4ade80;
	}

	.status-dot.composite {
		background: #f59e0b;
	}

	.info {
		display: flex;
		gap: 16px;
		margin-top: 20px;
		padding: 24px;
	}

	.info-icon {
		flex: 0 0 auto;
		width: 30px;
		height: 30px;
		display: grid;
		place-items: center;
		border-radius: 50%;
		background: #172554;
		color: #60a5fa;
		font-weight: 700;
	}

	.info h3 {
		margin: 0 0 7px;
		font-size: 14px;
	}

	.info p {
		margin: 0;
		color: #64748b;
		font-size: 13px;
		line-height: 1.6;
	}

	:global(.content > :global(div)) {
		margin-top: 30px;
	}

	@media (max-width: 650px) {
		.page {
			padding: 18px 14px 40px;
		}

		.hero {
			padding-top: 60px;
		}

		.hero h1 {
			letter-spacing: -2px;
		}

		.calculator-card,
		.results {
			padding: 20px;
		}

		.result-grid {
			grid-template-columns: 1fr;
		}

		.prime-card {
			grid-column: auto;
		}

		.version {		
                 display: none;
                 } 
        }         
 </style>
