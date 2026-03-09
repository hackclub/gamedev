<script lang="ts">
	let { children } = $props();
</script>

<svelte:head>
	<title>Hack Club Game Dev</title>
	<meta name="description" content="Hack Club is where high schoolers go from playing games to making games." />
	{@html '<style>@property --glow-r{syntax:"<number>";inherits:true;initial-value:0}@property --glow-g{syntax:"<number>";inherits:true;initial-value:0}@property --glow-b{syntax:"<number>";inherits:true;initial-value:0}</style>'}
</svelte:head>

{@render children()}

<style>
	@font-face {
		font-family: 'Zarathustra';
		src: url('/fonts/zarathustra.otf') format('opentype');
		font-weight: normal;
		font-style: normal;
		font-display: swap;
	}

	@font-face {
		font-family: 'Phantom Sans';
		src: url('https://assets.hackclub.com/fonts/Phantom_Sans_0.7/Regular.woff2') format('woff2'),
			url('https://assets.hackclub.com/fonts/Phantom_Sans_0.7/Regular.woff') format('woff');
		font-weight: normal;
		font-style: normal;
		font-display: swap;
	}

	@font-face {
		font-family: 'Phantom Sans';
		src: url('https://assets.hackclub.com/fonts/Phantom_Sans_0.7/Italic.woff2') format('woff2'),
			url('https://assets.hackclub.com/fonts/Phantom_Sans_0.7/Italic.woff') format('woff');
		font-weight: normal;
		font-style: italic;
		font-display: swap;
	}

	@font-face {
		font-family: 'Phantom Sans';
		src: url('https://assets.hackclub.com/fonts/Phantom_Sans_0.7/Bold.woff2') format('woff2'),
			url('https://assets.hackclub.com/fonts/Phantom_Sans_0.7/Bold.woff') format('woff');
		font-weight: bold;
		font-style: normal;
		font-display: swap;
	}

	:global(*) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	:global(html) {
		background: #000;
		overflow-x: hidden;
	}

	:global(body) {
		font-family: 'Phantom Sans', system-ui, -apple-system, sans-serif;
		color: #000;
		background: #fff;
		-webkit-font-smoothing: antialiased;
		overflow-x: hidden;
	}

	:global(a) {
		color: inherit;
		text-decoration: none;
	}

	:global(img) {
		max-width: 100%;
		height: auto;
		display: block;
	}

	:global(h1, h2, h3) {
		font-family: 'Zarathustra', Georgia, serif;
		font-weight: 400;
	}

	:global(button) {
		font-family: inherit;
		cursor: pointer;
	}
</style>
