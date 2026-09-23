```svelte
<script lang="ts">
	const name = 'Svelte';
	const easy = 'easy state management';
	const reactivity = 'reactivity without a virtual DOM';
</script>

<div class="footer">
	<h1>Hello {name}!</h1>

	<p>
		That’s it… Svelte is a worthy alternative to the currently popular
		options of <b>React</b>, <b>Vue</b>, and <b>Angular</b>. It has many
		benefits, including small bundle sizes, simple component definitions,
		{easy}, and {reactivity}.
	</p>

	<a href="https://svelte.dev" target="_blank" rel="noreferrer">
		Learn more about Svelte →
	</a>
</div>

<style>
	.footer {
		margin-top: 30px;
		padding: 28px;
		border: 1px solid #1e293b;
		border-radius: 24px;
		background: rgb(15 23 42 / 75%);
		box-shadow: 0 20px 70px rgb(0 0 0 / 20%);
		backdrop-filter: blur(20px);
	}

	h1 {
		margin: 0 0 18px;
		text-align: center;
		font-size: 22px;
		text-transform: uppercase;
		letter-spacing: 1px;
		color: #a78bfa;
	}

	p {
		margin: 0;
		color: #64748b;
		font-size: 13px;
		line-height: 1.8;
		text-align: justify;
	}

	a {
		display: inline-block;
		margin-top: 18px;
		color: #38bdf8;
		font-size: 13px;
		font-weight: 600;
		text-decoration: none;
		transition:
			color 0.2s ease,
			transform 0.2s ease;
	}

	a:hover {
		color: #a78bfa;
		transform: translateX(3px);
	}

	@media (max-width: 650px) {
		.footer {
			padding: 20px;
		}

		p {
			text-align: left;
		}
	}
</style>
```

