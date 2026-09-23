<script lang="ts">
	let name = $state('Svelte');
	let easy = $state('easy state management');
	let reactivity = $state('reactivity without a virtual DOM');
</script>

<style>
	div {
		border: 1px solid gray;
		padding: 8px;
	}

	h1 {
		text-align: center;
		text-transform: uppercase;
		color: #4caf50;
	}

	p {
		text-indent: 50px;
		text-align: justify;
		letter-spacing: 3px;
	}

	a {
		text-decoration: none;
		color: #008cba;
	}
</style>

<div>
	<h1>Hello {name}!</h1>

	<p>
		That’s it… Svelte is a worthy alternative to the currently popular
		options of <b>React</b>, <b>Vue</b>, and <b>Angular</b>. It has many
		benefits, including small bundle sizes, simple component definitions,
		{easy}, and {reactivity}.
	</p>
</div>


