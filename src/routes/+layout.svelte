<script lang="ts">
	let { children } = $props();

	const TITLE = 'Hack Club Game Dev — Real games built by teenagers';
	const DESCRIPTION =
		'Hack Club is where high schoolers become game developers. A global nonprofit running game jams like Juice, Daydream, and Campfire — see the real games teenagers have built.';
	const URL = 'https://gamedev.hackclub.com';
	const OG_IMAGE = 'https://gamedev.hackclub.com/ogimg.png';
	const OG_IMAGE_ALT =
		'A collage of game screenshots from games built by teenagers through Hack Club';

	const siteJsonLd = JSON.stringify({
		'@context': 'https://schema.org',
		'@graph': [
			{
				'@type': 'NonprofitOrganization',
				'@id': 'https://hackclub.com#organization',
				name: 'Hack Club',
				alternateName: 'The Hack Foundation',
				url: 'https://hackclub.com',
				logo: 'https://gamedev.hackclub.com/images/hc-logo.webp',
				description:
					'A global nonprofit movement of 140,000 teenagers making cool stuff together.',
				foundingDate: '2014',
				sameAs: ['https://github.com/hackclub', 'https://hackclub.com/slack']
			},
			{
				'@type': 'WebSite',
				'@id': `${URL}#website`,
				url: URL,
				name: 'Hack Club Game Dev',
				description: DESCRIPTION,
				publisher: { '@id': 'https://hackclub.com#organization' },
				inLanguage: 'en-US'
			}
		]
	}).replace(/</g, '\\u003c');
</script>

<svelte:head>
	<title>{TITLE}</title>
	<meta name="description" content={DESCRIPTION} />
	<link rel="canonical" href={URL} />
	<meta name="robots" content="index, follow, max-image-preview:large" />
	<meta name="author" content="Hack Club" />
	<meta name="application-name" content="Hack Club Game Dev" />
	<meta name="format-detection" content="telephone=no" />

	<!-- Open Graph -->
	<meta property="og:title" content={TITLE} />
	<meta property="og:description" content={DESCRIPTION} />
	<meta property="og:type" content="website" />
	<meta property="og:url" content={URL} />
	<meta property="og:image" content={OG_IMAGE} />
	<meta property="og:image:width" content="1200" />
	<meta property="og:image:height" content="630" />
	<meta property="og:image:alt" content={OG_IMAGE_ALT} />
	<meta property="og:site_name" content="Hack Club Game Dev" />
	<meta property="og:locale" content="en_US" />

	<!-- Twitter -->
	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:site" content="@hackclub" />
	<meta name="twitter:creator" content="@hackclub" />
	<meta name="twitter:title" content={TITLE} />
	<meta name="twitter:description" content={DESCRIPTION} />
	<meta name="twitter:image" content={OG_IMAGE} />
	<meta name="twitter:image:alt" content={OG_IMAGE_ALT} />

	<meta name="theme-color" content="#000000" />

	<link rel="preconnect" href="https://assets.hackclub.com" crossorigin="anonymous" />
	<link rel="preconnect" href="https://www.youtube.com" />

	{@html '<style>@property --glow-r{syntax:"<number>";inherits:true;initial-value:0}@property --glow-g{syntax:"<number>";inherits:true;initial-value:0}@property --glow-b{syntax:"<number>";inherits:true;initial-value:0}</style>'}
	{@html `<script type="application/ld+json">${siteJsonLd}</script>`}
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

	/* Visually hidden but readable by screen readers and crawlers */
	:global(.sr-only) {
		position: absolute;
		width: 1px;
		height: 1px;
		padding: 0;
		margin: -1px;
		overflow: hidden;
		clip: rect(0, 0, 0, 0);
		white-space: nowrap;
		border: 0;
	}
</style>
