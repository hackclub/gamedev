<script lang="ts">
	interface Game {
		title: string;
		authors: { name: string; age: number; location: string }[];
		description: string;
		image: string;
		thumbnail: string;
		playUrl: string;
		color: [number, number, number];
	}

	const games: Game[] = [
		{
			title: 'prode dies',
			authors: [{ name: 'Herby', age: 16, location: 'Canada' }],
			description: 'A visual novel about a teenager trying to solve their own murder.',
			image: '/images/prode-dies.webp', thumbnail: '/images/prode-dies.webp',
			playUrl: 'https://herbeon.itch.io/prode-dies', color: [106, 86, 191]
		},
		{
			title: 'Specter',
			authors: [{ name: 'Yessa', age: 18, location: 'Philippines' }],
			description: 'A platformer, where the ghost of your past run can help you finish the level or slow you down.',
			image: '/images/specter.webp', thumbnail: '/images/specter.webp',
			playUrl: 'https://shaaarkai.itch.io/specter', color: [191, 105, 86]
		},
		{
			title: 'DeathLeap',
			authors: [
				{ name: 'Noel', age: 16, location: 'Finland' },
				{ name: 'Isak', age: 17, location: 'Finland' },
				{ name: 'Aapo', age: 17, location: 'Finland' }
			],
			description: 'A puzzle platformer where you ruthlessly use the characters of the world as mere tools.',
			image: '/images/deathleap.webp', thumbnail: '/images/deathleap.webp',
			playUrl: 'https://qrosp-games-oy.itch.io/deathleap', color: [86, 164, 191]
		},
		{
			title: 'Kamikamace',
			authors: [
				{ name: 'Andromeda', age: 18, location: 'UK' },
				{ name: 'Nihaal', age: 16, location: 'UK' },
				{ name: 'Rimma', age: 15, location: 'US' }
			],
			description: 'A fast-paced PvP mace-swinging game where your goal is to die first.',
			image: '/images/kamikamace.webp', thumbnail: '/images/kamikamace.webp',
			playUrl: 'https://thatotherandrew.itch.io/kamikamace', color: [191, 89, 86]
		},
		{
			title: 'Voidwatch',
			authors: [{ name: 'Malcolm', age: 18, location: 'US' }],
			description: 'A fast-paced top-down space shooter roguelike.',
			image: '/images/voidwatch.webp', thumbnail: '/images/voidwatch.webp',
			playUrl: 'https://store.steampowered.com/app/3764010/Voidwatch/', color: [191, 86, 96]
		},
		{
			title: 'Speedtickers',
			authors: [
				{ name: 'Juan', age: 14, location: 'Argentina' },
				{ name: 'Agustin', age: 15, location: 'Argentina' }
			],
			description: 'A high-speed speedrun-focused platformer that pushes players to master momentum and precision.',
			image: '/images/speedtickers.webp', thumbnail: '/images/speedtickers.webp',
			playUrl: 'https://juanes10201.itch.io/speedtickers', color: [86, 111, 191]
		},
		{
			title: 'Bitdropper',
			authors: [{ name: 'Mari', age: 17, location: 'US' }],
			description: 'An arcade game — catch parts, and don\'t fall!',
			image: '/images/bitdropper.webp', thumbnail: '/images/bitdropper.webp',
			playUrl: 'https://kiptunes.itch.io/bitdropper', color: [191, 106, 86]
		},
		{
			title: 'More Scoops Plws',
			authors: [{ name: 'Rigo', age: 17, location: 'UAE' }],
			description: 'A game about serving scoops of ice cream to customers for points.',
			image: '/images/more-scoops-plws.webp', thumbnail: '/images/more-scoops-plws.webp',
			playUrl: 'https://recsaur.itch.io/more-scoops-plws', color: [191, 86, 155]
		},
		{
			title: 'Little Ducky',
			authors: [{ name: 'Leo', age: 16, location: 'US' }],
			description: 'An ASCII story-based exploration adventure game.',
			image: '/images/little-ducky.webp', thumbnail: '/images/little-ducky.webp',
			playUrl: 'https://littleducky.deltea.space', color: [191, 179, 86]
		},
		{
			title: 'Royally Unemployed',
			authors: [
				{ name: 'Julia', age: 17, location: 'US' },
				{ name: 'Shurui', age: 13, location: 'Australia' },
				{ name: 'Candy', age: 14, location: 'Malaysia' }
			],
			description: 'A story-rich turn-based battle game, made within 72 hours.',
			image: '/images/royally-unemployed.webp', thumbnail: '/images/royally-unemployed.webp',
			playUrl: 'https://solacye.itch.io/overglade', color: [86, 146, 191]
		},
		{
			title: 'Deadbeat',
			authors: [{ name: 'Augie', age: 17, location: 'US' }],
			description: 'A fast-paced top-down arena shooter with a rhythmic twist.',
			image: '/images/deadbeat.webp', thumbnail: '/images/deadbeat.webp',
			playUrl: 'https://gusruben.itch.io/deadbeat', color: [191, 86, 145]
		},
		{
			title: 'Gone Loopin\'',
			authors: [{ name: 'Tongyu', age: 18, location: 'Singapore' }],
			description: 'A game about fishing with a loop, made within 72 hours.',
			image: '/images/gone-loopin.webp', thumbnail: '/images/gone-loopin.webp',
			playUrl: 'https://bucketfish.itch.io/gone-loopin', color: [86, 141, 191]
		}
	];

	const SLOT_LEFT = [0, 168, 336, 944, 1112];
	const SLOT_WIDTH = [120, 120, 560, 120, 120];

	let currentGame = $state(0);
	let animPhase = $state<'idle' | 'animating'>('idle');
	let animDirection = $state<'left' | 'right' | null>(null);
	let prevIndices = $state<number[]>([]);
	let nextIndices = $state<number[]>([]);
	let windowWidth = $state(1400);

	function wrap(i: number) { return ((i % games.length) + games.length) % games.length; }

	let visibleIndices = $derived([-2, -1, 0, 1, 2].map(o => wrap(currentGame + o)));
	let spotColor = $derived(games[currentGame].color);

	function cartridgeBg(color: [number, number, number]) {
		return `linear-gradient(180deg, rgba(${color[0]},${color[1]},${color[2]},0.15), rgba(255,255,255,0.15))`;
	}

	function metaBg(color: [number, number, number]) {
		return `linear-gradient(to bottom, rgba(${color[0]},${color[1]},${color[2]},0.1), rgba(255,255,255,0.9))`;
	}

	const ANIM_DURATION = 550;

	async function navigate(direction: 'left' | 'right') {
		if (animPhase !== 'idle') return;

		const nextCenter = wrap(currentGame + (direction === 'right' ? 1 : -1));

		if (windowWidth <= 1200) {
			currentGame = nextCenter;
			return;
		}

		animDirection = direction;
		prevIndices = [...visibleIndices];
		nextIndices = [-2, -1, 0, 1, 2].map(o => wrap(nextCenter + o));

		animPhase = 'animating';
		await new Promise(r => setTimeout(r, ANIM_DURATION));
		currentGame = nextCenter;
		animPhase = 'idle';
		animDirection = null;
	}

	function handleKeydown(e: KeyboardEvent) {
		if (e.key === 'ArrowLeft') navigate('left');
		if (e.key === 'ArrowRight') navigate('right');
	}

	// Sticker dragging
	let topZ = $state(10);
	let draggingSticker = $state<string | null>(null);
	let dragStartPointer = { x: 0, y: 0 };
	let stickerOffsets: Record<string, { x: number; y: number }> = $state({});
	let stickerZ: Record<string, number> = $state({});

	function onStickerDown(e: PointerEvent, id: string) {
		e.preventDefault();
		const el = e.currentTarget as HTMLElement;
		el.setPointerCapture(e.pointerId);
		draggingSticker = id;
		topZ++;
		stickerZ[id] = topZ;
		const off = stickerOffsets[id] ?? { x: 0, y: 0 };
		dragStartPointer = { x: e.clientX - off.x, y: e.clientY - off.y };
	}

	function onStickerMove(e: PointerEvent) {
		if (!draggingSticker) return;
		stickerOffsets[draggingSticker] = {
			x: e.clientX - dragStartPointer.x,
			y: e.clientY - dragStartPointer.y
		};
	}

	function onStickerUp() {
		draggingSticker = null;
	}

	function stickerStyle(id: string) {
		const off = stickerOffsets[id];
		const z = stickerZ[id];
		let s = '';
		if (off) s += `translate: ${off.x}px ${off.y}px;`;
		if (z) s += `z-index: ${z};`;
		return s;
	}

	// Logo cell flash animation
	function flashCell(e: MouseEvent) {
		const el = e.currentTarget as HTMLElement;
		el.classList.remove('flash');
		void el.offsetWidth;
		el.classList.add('flash');
	}
</script>

<svelte:window bind:innerWidth={windowWidth} onkeydown={handleKeydown} />

{#snippet cartridgeInner(game: Game)}
	<div class="side-hline"></div>
	<div class="side-thumb-wrap"><img src={game.thumbnail} alt={game.title} /></div>
	<div class="side-bars">
		<div class="side-vbar"></div>
		<div class="side-vbar"></div>
		<div class="side-vbar"></div>
	</div>
{/snippet}

{#snippet spotlightInner(game: Game)}
	<div class="corner-dot tl"></div>
	<div class="corner-dot tr"></div>
	<div class="corner-dot bl"></div>
	<div class="corner-dot br"></div>
	<div class="game-cover" onclick={() => window.open(game.playUrl, '_blank')} role="link" tabindex="0">
		<img src={game.image} alt={game.title} />
	</div>
	<div class="game-meta-area" style="background:{metaBg(game.color)};">
		<h3 class="game-name">{game.title}</h3>
		<div class="game-byline">
			<span>By {game.authors.map(a => `${a.name}, ${a.age}`).join(' & ')}</span>
			<span class="meta-dot">&middot;</span>
			<span class="faded">from {[...new Set(game.authors.map(a => a.location))].join(' & ')}</span>
		</div>
		<p class="game-description">{game.description}</p>
	</div>
	<div class="game-nav">
		<button class="nav-cell nav-arrow-cell" onclick={() => navigate('left')}>
			<svg width="28" height="28" viewBox="0 0 28 28" fill="none"><path d="M18 4L8 14L18 24" stroke="#000" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
		</button>
		<button class="nav-cell nav-play-cell" onclick={() => window.open(game.playUrl, '_blank')}>
			<svg width="28" height="28" viewBox="0 0 28 28" fill="none"><path d="M8 4L24 14L8 24V4Z" fill="#000"/></svg>
		</button>
		<button class="nav-cell nav-arrow-cell" onclick={() => navigate('right')}>
			<svg width="28" height="28" viewBox="0 0 28 28" fill="none"><path d="M10 4L20 14L10 24" stroke="#000" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
		</button>
	</div>
{/snippet}

<!-- HERO SECTION -->
<section class="hero">
	<div class="hero-pattern"></div>
	<div class="hero-pattern-fade"></div>
	<div class="hero-games">
		<!-- Top-left cluster -->
		<img src="/images/hero-game-7.webp" alt="" class="game-shot g1" />
		<img src="/images/hero-game-8.webp" alt="" class="game-shot g2" />
		<img src="/images/hero-game-4.webp" alt="" class="game-shot g3" />
		<!-- Top-center-left -->
		<img src="/images/hero-game-10.webp" alt="" class="game-shot g4" />
		<!-- Top-center-right -->
		<img src="/images/hero-game-9.webp" alt="" class="game-shot g5" />
		<!-- Top-right cluster -->
		<img src="/images/hero-game-11.webp" alt="" class="game-shot g6" />
		<img src="/images/hero-game-12.webp" alt="" class="game-shot g7" />
		<img src="/images/hero-game-3.webp" alt="" class="game-shot g8" />
		<!-- Left middle -->
		<img src="/images/hero-game-1.webp" alt="" class="game-shot g9" />
		<img src="/images/hero-game-2.webp" alt="" class="game-shot g10" />
		<!-- Right middle -->
		<img src="/images/hero-game-5.webp" alt="" class="game-shot g11" />
		<img src="/images/hero-game-6.webp" alt="" class="game-shot g12" />
		<!-- Left lower -->
		<img src="/images/additional1.webp" alt="" class="game-shot g19" />
		<!-- Right lower -->
		<img src="/images/additional2.webp" alt="" class="game-shot g20" />
		<!-- Top fill gaps -->
		<img src="/images/additional3.webp" alt="" class="game-shot g21" />
		<img src="/images/additional4.webp" alt="" class="game-shot g22" />
		<img src="/images/additional5.webp" alt="" class="game-shot g23" />
		<!-- Bottom-left (sloping inward) -->
		<img src="/images/additional6.webp" alt="" class="game-shot g13" />
		<img src="/images/additional7.webp" alt="" class="game-shot g14" />
		<img src="/images/additional8.webp" alt="" class="game-shot g15" />
		<!-- Bottom-right (sloping inward) -->
		<img src="/images/additional9.webp" alt="" class="game-shot g16" />
		<img src="/images/additional10.webp" alt="" class="game-shot g17" />
		<img src="/images/additional11.webp" alt="" class="game-shot g18" />
	</div>
	<div class="hero-content">
		<p class="hero-heading-top">
			Hack Club is where <span class="underlined">high&nbsp;schoolers</span><br />
			go from playing games
		</p>
		<h1 class="hero-heading-big">to making games.</h1>
		<div class="hero-cta">
			<a href="#donate" class="btn-pill">Donate</a>
		</div>
		<a href="https://hackclub.com/slack" class="hero-join">Teenager? Join Hack Club!</a>
		<div class="hero-arrow">
			<svg width="40" height="20" viewBox="0 0 40 20" fill="none">
				<path d="M2 2L20 16L38 2" stroke="#ec3750" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
			</svg>
		</div>
	</div>
</section>

<!-- FULL-WIDTH BORDERED AREA -->
<div class="bordered-wrapper">
	<!-- Decorative tiled pattern outside content -->
	<div class="side-pattern left-pattern"></div>
	<div class="side-pattern right-pattern"></div>

	<!-- Vertical border lines -->
	<div class="border-line left-line"></div>
	<div class="border-line right-line"></div>

	<!-- Dot at top of lines -->
	<div class="line-dot dot-top-left"></div>
	<div class="line-dot dot-top-right"></div>

	<!-- ABOUT BLURB (outside bordered-content so it can layer above border lines) -->
	<div class="about-blurb">
		<div class="line-dot" style="top:-5px;left:-5px;"></div>
		<div class="line-dot" style="top:-5px;right:-5px;"></div>
		<div class="line-dot" style="bottom:-5px;left:-5px;"></div>
		<div class="line-dot" style="bottom:-5px;right:-5px;"></div>
		<p><a href="https://hackclub.com" target="_blank">Hack Club</a> is a global nonprofit movement of 140,000 teenagers making cool stuff together. Every couple of weeks, we run events to empower and encourage students to dive deeper into game development.<br><br>Share this page with <a href="https://hack.club/games" style="text-decoration: underline; font-weight: normal">hack.club/games</a>.</p>
	</div>

	<div class="bordered-content">

		<!-- ====== JUICE SECTION ====== -->
		<section class="event-section">
			<div class="event-grid juice-grid">
				<!-- LEFT: Two stacked photos -->
				<div class="photo-stack">
					<div class="stack-photo"><img src="/images/juice-7.webp" alt="Juice group photo" /></div>
					<div class="stack-photo"><img src="/images/juice-2.webp" alt="Juice whiteboard" /></div>
				</div>
				<!-- Vertical divider -->
				<div class="grid-divider">
					<div class="line-dot" style="top:-4px;left:-4px;"></div>
					<div class="line-dot" style="bottom:-4px;left:-4px;"></div>
				</div>
				<!-- RIGHT: Open space on top, photos row below -->
				<div class="event-right-col">
					<div class="event-open-space">
						<div class="event-columns">
							<div class="event-text-block">
								<h2 class="event-title">Juice</h2>
								<p class="event-desc">100 teenagers built a game in two months, then ran a popup cafe in Shanghai for seven days.</p>
							</div>
							<div class="event-video-col">
								<div class="video-thumb">
									<div class="corner-dot tl"></div>
									<div class="corner-dot tr"></div>
									<div class="corner-dot bl"></div>
									<div class="corner-dot br"></div>
									<iframe
										width="354"
										height="200"
										src="https://www.youtube.com/embed/Gtjyyu82pw4"
										title="Juice video"
										frameborder="0"
										allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
										allowfullscreen
									></iframe>
								</div>
								<span class="watch-label">watch the video <span class="watch-arrow">↗</span></span>
							</div>
						</div>
						<!-- Stickers cluster -->
						<div class="sticker-cluster">
							<img src="/images/sticker-holo-1.webp" alt="" class="sticker s1" class:dragging={draggingSticker === 'j1'} style={stickerStyle('j1')} draggable="false" onpointerdown={(e) => onStickerDown(e, 'j1')} onpointermove={onStickerMove} onpointerup={onStickerUp} />
							<img src="/images/sticker-1.webp" alt="" class="sticker s2" class:dragging={draggingSticker === 'j2'} style={stickerStyle('j2')} draggable="false" onpointerdown={(e) => onStickerDown(e, 'j2')} onpointermove={onStickerMove} onpointerup={onStickerUp} />
							<img src="/images/sticker-2.webp" alt="" class="sticker s3" class:dragging={draggingSticker === 'j3'} style={stickerStyle('j3')} draggable="false" onpointerdown={(e) => onStickerDown(e, 'j3')} onpointermove={onStickerMove} onpointerup={onStickerUp} />
							<img src="/images/sticker-3-holo.webp" alt="" class="sticker s4" class:dragging={draggingSticker === 'j4'} style={stickerStyle('j4')} draggable="false" onpointerdown={(e) => onStickerDown(e, 'j4')} onpointermove={onStickerMove} onpointerup={onStickerUp} />
						</div>
					</div>
					<div class="event-photo-row">
						<div class="row-photo"><img src="/images/juice-3.webp" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-4.webp" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-5.webp" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-6.webp" alt="" /></div>
						<!-- <div class="row-photo"><img src="/images/juice-7.webp" alt="" /></div> -->
					</div>
				</div>
			</div>
			<div class="line-dot" style="top:-4px;left:-4px;"></div>
			<div class="line-dot" style="top:-4px;right:-4px;"></div>
			<div class="line-dot" style="bottom:-4px;left:-4px;"></div>
			<div class="line-dot" style="bottom:-4px;right:-4px;"></div>
		</section>

		<!-- MARQUEE 1 -->
		<div class="marquee-section">
			<div class="marquee-line-left"></div>
			<div class="marquee-line-right"></div>
			<div class="marquee-clip">
				<div class="marquee-fade left"></div>
				<div class="marquee-fade right"></div>
				<div class="marquee-track">
					{#each Array(30) as _}
						<span class="marquee-word">teens inspiring</span>
					{/each}
				</div>
			</div>
		</div>

		<!-- ====== DAYDREAM SECTION (flipped) ====== -->
		<section class="event-section">
			<div class="event-grid daydream-grid">
				<!-- LEFT: Open space on top, photos row below -->
				<div class="event-right-col">
					<div class="event-open-space">
						<div class="event-columns daydream-columns">
							<div class="event-text-block">
								<h2 class="event-title">Daydream</h2>
								<p class="event-desc">100 high school game jams in 100 cities around the world, all on the same weekend</p>
							</div>
							<div class="event-video-col">
								<div class="video-thumb">
									<div class="corner-dot tl"></div>
									<div class="corner-dot tr"></div>
									<div class="corner-dot bl"></div>
									<div class="corner-dot br"></div>
									<iframe
										width="354"
										height="200"
										src="https://www.youtube.com/embed/vvdoW2gh9YU"
										title="Daydream video"
										frameborder="0"
										allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
										allowfullscreen
									></iframe>
								</div>
								<span class="watch-label">watch the video <span class="watch-arrow">↗</span></span>
							</div>
						</div>
						<div class="sticker-cluster">
							<img src="/images/daydream-sticker-1.webp" alt="" class="sticker s1" class:dragging={draggingSticker === 'd1'} style={stickerStyle('d1')} draggable="false" onpointerdown={(e) => onStickerDown(e, 'd1')} onpointermove={onStickerMove} onpointerup={onStickerUp} />
							<img src="/images/daydream-sticker-2.webp" alt="" class="sticker s2" class:dragging={draggingSticker === 'd2'} style={stickerStyle('d2')} draggable="false" onpointerdown={(e) => onStickerDown(e, 'd2')} onpointermove={onStickerMove} onpointerup={onStickerUp} />
							<img src="/images/daydream-sticker-3.webp" alt="" class="sticker s3" class:dragging={draggingSticker === 'd3'} style={stickerStyle('d3')} draggable="false" onpointerdown={(e) => onStickerDown(e, 'd3')} onpointermove={onStickerMove} onpointerup={onStickerUp} />
						</div>
					</div>
					<div class="event-photo-row">
						<div class="row-photo"><img src="/images/daydream-2.webp" alt="" /></div>
						<div class="row-photo"><img src="/images/daydream-3.webp" alt="" /></div>
						<div class="row-photo"><img src="/images/daydream-5.webp" alt="" /></div>
						<!-- <div class="row-photo"><img src="/images/juice-8.webp" alt="" /></div> -->
					</div>
				</div>
				<!-- Vertical divider -->
				<div class="grid-divider">
					<div class="line-dot" style="top:-4px;left:-4px;"></div>
					<div class="line-dot" style="bottom:-4px;left:-4px;"></div>
				</div>
				<!-- RIGHT: Two stacked photos -->
				<div class="photo-stack">
					<div class="stack-photo"><img src="/images/daydream-1.webp" alt="Daydream group photo" /></div>
					<div class="stack-photo"><img src="/images/daydream-4.webp" alt="Daydream whiteboard" /></div>
				</div>
			</div>
			<div class="line-dot" style="top:-4px;left:-4px;"></div>
			<div class="line-dot" style="top:-4px;right:-4px;"></div>
			<div class="line-dot" style="bottom:-4px;left:-4px;"></div>
			<div class="line-dot" style="bottom:-4px;right:-4px;"></div>
		</section>

		<!-- MARQUEE 2 -->
		<div class="marquee-section">
			<div class="marquee-line-left"></div>
			<div class="marquee-line-right"></div>
			<div class="marquee-clip">
				<div class="marquee-fade left"></div>
				<div class="marquee-fade right"></div>
				<div class="marquee-track reverse">
					{#each Array(30) as _}
						<span class="marquee-word">play to make to</span>
					{/each}
				</div>
			</div>
		</div>

		<!-- ====== THREE-COLUMN EVENTS ====== -->
		<section class="event-section three-col-section">
			<div class="three-col-grid">
				<div class="three-col-cell">
					<div class="col-tint lavender"></div>
					<div class="col-inner">
						<div class="video-thumb col-thumb">
							<div class="corner-dot tl"></div>
							<div class="corner-dot tr"></div>
							<div class="corner-dot bl"></div>
							<div class="corner-dot br"></div>
							<img src="/images/campfire-flagship.webp" alt="Campfire Flagship" />
						</div>
						<h3 class="col-title">Campfire Flagship</h3>
						<p class="col-desc">Partnered with <a href="https://opensauce.com" target="_blank" style="text-decoration: underline">Open Sauce</a>, 75 teens made games under the guidance of popular creators like Michael Reeves in Los Angeles.</p>
					</div>
				</div>
				<div class="col-divider-v"></div>
				<div class="three-col-cell">
					<div class="col-tint cyan"></div>
					<div class="col-inner">
						<div class="video-thumb col-thumb">
							<div class="corner-dot tl"></div>
							<div class="corner-dot tr"></div>
							<div class="corner-dot bl"></div>
							<div class="corner-dot br"></div>
							<img src="/images/overglade.webp" alt="Overglade" />
						</div>
						<h3 class="col-title">Overglade</h3>
						<p class="col-desc">50 teenagers built games in three months, then flew to Singapore for an immersive, alternate-reality game jam over four days.</p>
					</div>
				</div>
				<div class="col-divider-v"></div>
				<div class="three-col-cell">
					<div class="col-tint orange"></div>
					<div class="col-inner">
						<div class="video-thumb col-thumb">
							<div class="corner-dot tl"></div>
							<div class="corner-dot tr"></div>
							<div class="corner-dot bl"></div>
							<div class="corner-dot br"></div>
							<img src="/images/campfire-grid.webp" alt="Campfire" />
						</div>
						<h3 class="col-title">Campfire Global</h3>
						<p class="col-desc">Our largest game jam yet — 200 high school game jams in 200 cities around the world, all on the same weekend.</p>
					</div>
				</div>
			</div>
			<div class="line-dot" style="top:-4px;left:-4px;"></div>
			<div class="line-dot" style="top:-4px;right:-4px;"></div>
			<div class="line-dot" style="bottom:-4px;left:-4px;"></div>
			<div class="line-dot" style="bottom:-4px;right:-4px;"></div>
		</section>

		<!-- REAL GAMES HEADING (inside bordered area) -->
		<div class="games-heading-area">
			<div class="games-heading-glow" style="--glow-r:{spotColor[0]};--glow-g:{spotColor[1]};--glow-b:{spotColor[2]};"></div>
			<h2 class="games-heading">Real games built by teenagers</h2>
			<p class="games-sub">Don't take our word for it — see for yourself.</p>
		</div>

	</div>

	<!-- Dot at bottom of lines -->
	<div class="line-dot dot-bottom-left"></div>
	<div class="line-dot dot-bottom-right"></div>
</div>

<!-- FULL-WIDTH GAMES SHOWCASE -->
<div class="games-full-section">
	<section class="games-showcase">
		<div class="games-carousel" class:animating={animPhase !== 'idle'}>
			{#if animPhase === 'idle'}
				<!-- ===== IDLE STATE: 5 static cards ===== -->
				{#each [0, 1, 3, 4] as slot}
					{@const game = games[visibleIndices[slot]]}
					<div
						class="side-card"
						style="position:absolute; left:{SLOT_LEFT[slot]}px; top:0; bottom:0; width:120px; background:{cartridgeBg(game.color)};"
					>
						{@render cartridgeInner(game)}
					</div>
				{/each}
				{@const spotGame = games[visibleIndices[2]]}
				<div class="main-game-card" style="position:absolute; left:336px; top:0; bottom:0; width:560px;">
					{@render spotlightInner(spotGame)}
				</div>

			{:else if animDirection === 'right'}
				<!-- ===== NAVIGATE RIGHT ANIMATION ===== -->

				<!-- Flip pair 1: Spotlight → Cartridge (immediate) -->
				<!-- Hinge at 336, slides left 48px. Edge cards nested to track the new cartridge unfolding. -->
				{@const fp1 = games[prevIndices[2]]}
				{@const g1 = games[prevIndices[1]]}
				{@const g0 = games[prevIndices[0]]}
				<div class="flip-pair anim-flip-	lide-left" style="position:absolute; left:336px; top:0; bottom:0;">
					<div class="main-game-card flip-old-nr" style="position:absolute; left:0; top:0; bottom:0; width:560px;">
						{@render spotlightInner(fp1)}
					</div>
					<div class="side-card flip-new-nr" style="position:absolute; right:0; top:0; bottom:0; width:120px; background:{cartridgeBg(fp1.color)};">
						{@render cartridgeInner(fp1)}
					</div>
					<!-- Slot 1: tracks new cartridge's left edge unfolding -->
					<div class="side-card edge-unfold-left" style="position:absolute; left:-168px; top:0; bottom:0; width:120px; background:{cartridgeBg(g1.color)};">
						{@render cartridgeInner(g1)}
					</div>
					<!-- Slot 0: same tracking + fade out (staggered, further travel) -->
					<div class="side-card edge-exit-unfold-left edge-outer" style="position:absolute; left:-336px; top:0; bottom:0; width:120px; background:{cartridgeBg(g0.color)};">
						{@render cartridgeInner(g0)}
					</div>
				</div>

				<!-- Flip pair 2: Cartridge → Spotlight (delayed) -->
				<!-- Hinge at 944, slides left 48px. Edge cards nested to track the old cartridge folding away. -->
				{@const fp2 = games[prevIndices[3]]}
				{@const g4 = games[prevIndices[4]]}
				{@const gn = games[nextIndices[4]]}
				<div class="flip-pair anim-flip-slide-left anim-delayed" style="position:absolute; left:944px; top:0; bottom:0;">
					<div class="side-card flip-old-nr anim-delayed" style="position:absolute; left:0; top:0; bottom:0; width:120px; background:{cartridgeBg(fp2.color)};">
						{@render cartridgeInner(fp2)}
					</div>
					<div class="main-game-card flip-new-nr anim-delayed" style="position:absolute; right:0; top:0; bottom:0; width:560px;">
						{@render spotlightInner(fp2)}
					</div>
					<!-- Slot 4: tracks old cartridge's right edge folding away -->
					<div class="side-card edge-fold-left anim-delayed" style="position:absolute; left:168px; top:0; bottom:0; width:120px; background:{cartridgeBg(g4.color)};">
						{@render cartridgeInner(g4)}
					</div>
					<!-- New card: same tracking + fade in (staggered, further travel) -->
					<div class="side-card edge-enter-fold-left anim-delayed edge-outer" style="position:absolute; left:416px; top:0; bottom:0; width:120px; background:{cartridgeBg(gn.color)};">
						{@render cartridgeInner(gn)}
					</div>
				</div>

			{:else}
				<!-- ===== NAVIGATE LEFT ANIMATION ===== -->

				<!-- Flip pair 1: Spotlight → Cartridge (immediate) -->
				<!-- Hinge at 896, slides right 48px. Edge cards track the new cartridge unfolding. -->
				{@const fp1l = games[prevIndices[2]]}
				{@const g3l = games[prevIndices[3]]}
				{@const g4l = games[prevIndices[4]]}
				<div class="flip-pair anim-flip-slide-right" style="position:absolute; left:896px; top:0; bottom:0;">
					<div class="main-game-card flip-old-nl" style="position:absolute; right:0; top:0; bottom:0; width:560px;">
						{@render spotlightInner(fp1l)}
					</div>
					<div class="side-card flip-new-nl" style="position:absolute; left:0; top:0; bottom:0; width:120px; background:{cartridgeBg(fp1l.color)};">
						{@render cartridgeInner(fp1l)}
					</div>
					<!-- Slot 3: tracks new cartridge's right edge unfolding -->
					<div class="side-card edge-unfold-right" style="position:absolute; left:48px; top:0; bottom:0; width:120px; background:{cartridgeBg(g3l.color)};">
						{@render cartridgeInner(g3l)}
					</div>
					<!-- Slot 4: same tracking + fade out (staggered, further travel) -->
					<div class="side-card edge-exit-unfold-right edge-outer" style="position:absolute; left:216px; top:0; bottom:0; width:120px; background:{cartridgeBg(g4l.color)};">
						{@render cartridgeInner(g4l)}
					</div>
				</div>

				<!-- Flip pair 2: Cartridge → Spotlight (delayed) -->
				<!-- Hinge at 288, slides right 48px. Edge cards track the old cartridge folding away. -->
				{@const fp2l = games[prevIndices[1]]}
				{@const g0l = games[prevIndices[0]]}
				{@const gnl = games[nextIndices[0]]}
				<div class="flip-pair anim-flip-slide-right anim-delayed" style="position:absolute; left:288px; top:0; bottom:0;">
					<div class="side-card flip-old-nl anim-delayed" style="position:absolute; right:0; top:0; bottom:0; width:120px; background:{cartridgeBg(fp2l.color)};">
						{@render cartridgeInner(fp2l)}
					</div>
					<div class="main-game-card flip-new-nl anim-delayed" style="position:absolute; left:0; top:0; bottom:0; width:560px;">
						{@render spotlightInner(fp2l)}
					</div>
					<!-- Slot 0: tracks old cartridge's left edge folding away -->
					<div class="side-card edge-fold-right anim-delayed" style="position:absolute; left:-288px; top:0; bottom:0; width:120px; background:{cartridgeBg(g0l.color)};">
						{@render cartridgeInner(g0l)}
					</div>
					<!-- New card: same tracking + fade in (staggered, further travel) -->
					<div class="side-card edge-enter-fold-right anim-delayed edge-outer" style="position:absolute; left:-536px; top:0; bottom:0; width:120px; background:{cartridgeBg(gnl.color)};">
						{@render cartridgeInner(gnl)}
					</div>
				</div>
			{/if}
		</div>
	</section>
</div>

<!-- DONATE SECTION -->
<div class="donate-bordered-wrapper">
	<!-- Decorative tiled pattern outside content -->
	<div class="side-pattern left-pattern"></div>
	<div class="side-pattern right-pattern"></div>
	<!-- Vertical border lines -->
	<div class="border-line left-line"></div>
	<div class="border-line right-line"></div>
	<!-- Dots -->
	<div class="line-dot dot-top-left"></div>
	<div class="line-dot dot-top-right"></div>
	<div class="line-dot dot-bottom-left"></div>
	<div class="line-dot dot-bottom-right"></div>

	<section class="donate-section" id="donate">
		<div class="donate-heading-area">
			<div class="donate-heading-glow" style="--glow-r:{spotColor[0]};--glow-g:{spotColor[1]};--glow-b:{spotColor[2]};"></div>
			<h2 class="donate-heading">Help a high schooler become<br/>a game developer</h2>
		</div>
		<div class="donate-columns">
			<div class="donate-col">
				<div class="donate-col-pattern"></div>
				<div class="donate-col-inner">
					<h3 class="donate-col-title">Contribute financially</h3>
					<div class="donate-col-body">
						<p>Every donation will go directly into towards encouraging teenagers to build games.</p>
						<p><strong>$100</strong> = a Steam license to publish a video game<br/>
						<strong>$500</strong> = 1 ticket to a flagship hackathon<br/>
						<strong>$650</strong> = 1 ticket + round-trip ground transportation to a flagship hackathon<br/>
						<strong>$1500</strong> = 1 ticket + flight to a flagship hackathon</p>
						<p style="opacity: 0.5">All donations are 100% tax deductible. All of our finances are <a href="https://hcb.hackclub.com/hq" target="_blank" style="text-decoration:underline">open source</a>.</p>
					</div>
					<a href="https://hcb.hackclub.com/donations/start/gamedev-fund" class="btn-pill donate-btn">Donate</a>
				</div>
			</div>
			<div class="donate-divider"></div>
			<div class="donate-col">
				<div class="donate-col-pattern"></div>
				<div class="donate-col-inner">
					<h3 class="donate-col-title">Contribute in other ways</h3>
					<div class="donate-col-body">
						<p><strong>Donate your space</strong> — we're running huge in-person hackathons & <a href="https://campfire.hackclub.com/" target="_blank" style="text-decoration: underline">game jams across the world</a>, and we'd love to use your space!</p>
						<p><strong>Donate 30 minutes of your time</strong> — do you have interesting stories or insights that you'd be willing to share? we'd love to have you for an AMA, or list a 30-minute call with you as a prize!</p>
						<p><strong>Donate your game</strong> — do you have a published game? if you donate us bulk game keys, we'll use it to reward teenagers for making games!</p>
					</div>
					<a href="https://forms.hackclub.com/gamedev" class="btn-pill donate-btn">Donate</a>
				</div>
			</div>
		</div>
	</section>

	<!-- LOGO STRIP -->
	<div class="logo-strip">
		{#each ['255,0,0', '255,127,0', '255,220,0', '0,180,0', '0,100,255', '75,0,130', '148,0,211'] as color, i}
			<div class="logo-cell" style="--cell-r-g-b:{color};" onmouseenter={flashCell}>
				<div class="logo-cell-pattern" style="background-image: linear-gradient(0deg, rgba(255,255,255,0) 0%, rgba(255,255,255,1) 100%), url('/images/patterns/pattern{i + 1}.svg');{i === 0 ? ' transform: scaleX(-1);' : ''}"></div>
			</div>
		{/each}
	</div>
</div>

<!-- FOOTER -->
<footer class="footer">
	<div class="footer-black-line"></div>
	<div class="footer-white-line"></div>
	<div class="footer-top">
		<p class="footer-tagline">Made with &lt;3 by teenagers, for teenagers</p>
		<nav class="footer-links">
			<a href="https://hackclub.com">Hack Club</a>
			<span class="footer-dot">∙</span>
			<a href="https://hackclub.com/slack">Slack</a>
			<span class="footer-dot">∙</span>
			<a href="https://hackclub.com/clubs">Clubs</a>
			<span class="footer-dot">∙</span>
			<a href="https://hackclub.com/hackathons">Hackathons</a>
		</nav>
		{#if Math.random() < 0.5}
			<p class="footer-credit">Site by <a href="https://github.com/gusruben/">Augie</a> & <a href="https://tongyu.dev/">Tongyu</a></p>
		{:else}
			<p class="footer-credit">Site by <a href="https://tongyu.dev/">Tongyu</a> & <a href="https://github.com/gusruben/">Augie</a></p>
		{/if}
	</div>
	<div class="footer-tile"></div>
</footer>

<style>
	/* Border thickness constant */
	:root { --b: 2px; }

	/* ===== HERO ===== */
	.hero {
		position: relative;
		width: 100%;
		height: 100vh;
		min-height: 700px;
		max-height: 1205px;
		overflow: hidden;
		background: #fff;
		box-shadow: 0 -100vh 0 100vh #fff;
	}

	.hero-pattern {
		position: absolute;
		inset: 0;
		background: url('/images/patterns/pattern5.svg') repeat;
		background-size: 40px 40px;
		opacity: 0.025;
		pointer-events: none;
	}

	.hero-pattern-fade {
		position: absolute;
		inset: 0;
		background: linear-gradient(to bottom, #fff 0%, transparent 100%);
		pointer-events: none;
	}

	.hero-games { position: absolute; inset: 0; pointer-events: none; }

	.game-shot {
		position: absolute;
		width: 300px;
		height: 225px;
		border: 5px solid #fff;
		border-radius: 8px;
		object-fit: cover;
		box-shadow: 0 4px 20px rgba(0,0,0,0.15);
	}

	/* Top-left cluster */
	.g1  { left: -60px;  top: -30px;  transform: rotate(-8deg);  z-index: 2; }
	.g2  { left: 110px;  top: -50px;  transform: rotate(5deg);   z-index: 1; }
	.g3  { left: 10px;   top: 100px;  transform: rotate(3deg);   z-index: 3; }
	/* Top-center-left */
	.g4  { left: 28%;    top: -60px;  transform: rotate(-3deg);  z-index: 1; }
	/* Top-center-right */
	.g5  { right: 28%;   top: -55px;  transform: rotate(-4deg);  z-index: 1; }
	/* Top-right cluster */
	.g6  { right: -40px; top: -40px;  transform: rotate(8deg);   z-index: 2; }
	.g7  { right: 120px; top: -50px;  transform: rotate(2deg);   z-index: 1; }
	.g8  { right: -60px; top: 110px;  transform: rotate(-6deg);  z-index: 3; }
	/* Left middle */
	.g9  { left: -80px;  top: 35%;    transform: rotate(-5deg);  z-index: 2; }
	.g10 { left: -40px;  top: 52%;    transform: rotate(4deg);   z-index: 3; }
	/* Right middle */
	.g11 { right: -80px; top: 35%;    transform: rotate(-3deg);  z-index: 2; }
	.g12 { right: -40px; top: 52%;    transform: rotate(8deg);   z-index: 3; }
	/* Bottom-left (sloping inward) */
	.g13 { left: -50px;  bottom: -10px; transform: rotate(6deg);  z-index: 3; }
	.g14 { left: 100px;  bottom: -30px; transform: rotate(-4deg); z-index: 4; }
	.g15 { left: 260px;  bottom: -50px; transform: rotate(3deg);  z-index: 3; }
	/* Bottom-right (sloping inward) */
	.g16 { right: -50px; bottom: -10px; transform: rotate(4deg);  z-index: 3; }
	.g17 { right: 100px; bottom: -30px; transform: rotate(-6deg); z-index: 4; }
	.g18 { right: 260px; bottom: -50px; transform: rotate(3deg);  z-index: 3; }
	/* Left lower (between middle and bottom) */
	.g19 { left: 120px;  top: 68%;     transform: rotate(7deg);   z-index: 3; }
	/* Right lower (between middle and bottom) */
	.g20 { right: 120px; top: 68%;     transform: rotate(-3deg);  z-index: 3; }
	/* Top fill gaps */
	.g21 { left: 22%;    top: -160px;  transform: rotate(-5deg);  z-index: 2; }
	.g22 { left: 44%;    top: -170px;  transform: rotate(2deg);   z-index: 2; }
	.g23 { right: 22%;   top: -155px;  transform: rotate(-6deg);  z-index: 2; }

	.hero-content {
		position: relative;
		z-index: 2;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: flex-end;
		height: 100%;
		text-align: center;
		padding-bottom: 120px;
	}

	.hero-heading-top {
		font-family: 'Phantom Sans', sans-serif;
		font-size: 48px;
		font-weight: 400;
		line-height: 1.3;
	}

	.underlined {
		position: relative;
		display: inline;
	}

	.underlined::after {
		content: '';
		position: absolute;
		left: -6px;
		right: 0;
		bottom: -6px;
		height: 22px;
		background: url('/images/underline.svg') no-repeat center;
		background-size: 100% 100%;
		z-index: -1;
	}

	.hero-heading-big {
		font-family: 'Zarathustra', Georgia, serif;
		font-size: 88px;
		font-weight: 400;
		line-height: 1.1;
		margin: 8px 0 32px;
	}

	.hero-cta { margin-bottom: 16px; }

	.btn-pill {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		width: 200px;
		height: 66px;
		border: var(--b) solid #000;
		border-radius: 999px;
		font-family: 'Phantom Sans', sans-serif;
		font-size: 20px;
		color: #000;
		background: #fff;
		cursor: pointer;
		transition: background 0.2s, color 0.2s;
		text-decoration: none;
	}

	.btn-pill:hover { background: #000; color: #fff; }

	.hero-join {
		font-size: 20px;
		opacity: 0.6;
		margin-top: 16px;
		margin-bottom: 32px;
		text-decoration: underline;
		color: inherit;
	}

	.hero-arrow {
		opacity: 0.8;
		position: relative;
		top: 32px;
		animation: hero-arrow-float 5s cubic-bezier(0.45, 0, 0.55, 1) infinite;
	}

	@keyframes hero-arrow-float {
		0% { transform: translateY(0); }
		50% { transform: translateY(5px); }
		100% { transform: translateY(0); }
	}

	/* ===== ABOUT BLURB ===== */
	.about-blurb {
		background: #fff;
		padding: 72px 80px;
		margin: 0 138px;
		border: var(--b) solid #000;
		position: relative;
		z-index: 6;
		text-align: center;
		font-size: 22px;
		line-height: 1.6;
	}

	.about-blurb a {
		text-decoration: underline;
		font-weight: 600;
	}

	/* ===== BORDERED WRAPPER ===== */
	.bordered-wrapper {
		position: relative;
		max-width: 1440px;
		margin: 0 auto;
	}

	/* Full-width top line via pseudo */
	.bordered-wrapper::before {
		content: '';
		position: absolute;
		top: 0;
		left: 50%;
		transform: translateX(-50%);
		width: 100vw;
		height: var(--b);
		background: #000;
		z-index: 4;
	}

	.bordered-wrapper::after {
		content: '';
		position: absolute;
		bottom: 0;
		left: 50%;
		transform: translateX(-50%);
		width: 100vw;
		height: var(--b);
		background: #000;
		z-index: 4;
	}

	.side-pattern {
		position: absolute;
		top: 0;
		bottom: 0;
		background: url('/images/stripe-pattern.svg') repeat;
		background-size: 64px 64px;
		opacity: 0.1;
		pointer-events: none;
		z-index: 1;
	}

	.left-pattern { left: -100vw; right: calc(100% - 160px); }
	.right-pattern { right: -100vw; left: calc(100% - 160px); }

	.border-line {
		position: absolute;
		top: 0;
		bottom: 0;
		width: var(--b);
		background: #000;
		z-index: 3;
	}

	.left-line { left: 160px; }
	.right-line { right: 160px; }

	.line-dot {
		position: absolute;
		width: 9px;
		height: 9px;
		background: #000;
		z-index: 5;
	}

	.dot-top-left { top: 0; left: 156px; }
	.dot-top-right { top: 0; right: 156px; }
	.dot-bottom-left { bottom: 0; left: 156px; }
	.dot-bottom-right { bottom: 0; right: 156px; }

	.bordered-content {
		position: relative;
		margin: 0 162px;
		z-index: 2;
	}

	/* First section's top border overlaps the about-blurb's bottom border */
	.bordered-content > :first-child {
		border-top: none;
	}

	/* ===== EVENT SECTIONS ===== */
	.event-section {
		position: relative;
		border-top: var(--b) solid #000;
		border-bottom: var(--b) solid #000;
		margin-top: calc(-1 * var(--b));
		overflow: visible;
	}

	.event-section:first-child {
		margin-top: 0;
	}

	.event-grid {
		display: grid;
		min-height: 550px;
		overflow: hidden;
	}

	.juice-grid {
		grid-template-columns: 30% var(--b) 1fr;
	}

	.daydream-grid {
		grid-template-columns: 1fr var(--b) 30%;
	}

	.grid-divider {
		background: #000;
		position: relative;
	}

	/* Photo stack (two images stacked) */
	.photo-stack {
		display: flex;
		flex-direction: column;
		overflow: hidden;
		min-width: 0;
	}

	.stack-photo {
		flex: 1;
		overflow: hidden;
	}

	.stack-photo + .stack-photo {
		border-top: var(--b) solid #000;
	}

	.stack-photo img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		object-position: center;
		display: block;
	}

	/* Right column: open space + photo row */
	.event-right-col {
		display: flex;
		flex-direction: column;
	}

	.event-open-space {
		flex: 1;
		position: relative;
		padding: 36px;
		overflow: hidden;
		min-height: 300px;
	}

	/* Two-column layout: text left, video right */
	.event-columns {
		display: flex;
		gap: 24px;
		position: relative;
		z-index: 2;
	}

	.daydream-columns {
		flex-direction: row;
	}

	.event-text-block {
		flex: 1;
		min-width: 0;
	}

	.event-video-col {
		flex-shrink: 0;
		padding-top: 8px;
		display: flex;
		flex-direction: column;
		align-items: flex-start;
	}

	.event-title {
		font-family: 'Zarathustra', Georgia, serif;
		font-size: 50px;
		font-weight: 400;
		margin-bottom: 18px;
	}

	.event-desc {
		font-size: 24px;
		line-height: 1.45;
		max-width: 290px;
	}

	.video-thumb {
		position: relative;
		border: var(--b) solid #000;
		display: inline-block;
	}

	.video-thumb img,
	.video-thumb iframe {
		display: block;
		width: 354px;
		height: 200px;
		object-fit: cover;
	}

	.corner-dot {
		position: absolute;
		width: 9px;
		height: 9px;
		background: #000;
		z-index: 5;
	}

	.corner-dot.tl { top: -5px; left: -5px; }
	.corner-dot.tr { top: -5px; right: -5px; }
	.corner-dot.bl { bottom: -5px; left: -5px; }
	.corner-dot.br { bottom: -5px; right: -5px; }

	.watch-label {
		display: inline-block;
		margin-top: 8px;
		font-size: 17px;
		opacity: 0.8;
		transform: rotate(3.9deg);
		transform-origin: left center;
	}

	/* Sticker cluster - absolutely positioned in bottom corner, clipped by overflow:hidden */
	.sticker-cluster {
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		z-index: 2;
		height: 120px;
		pointer-events: none;
	}

	.sticker {
		position: absolute;
		filter: drop-shadow(2px 3px 6px rgba(0,0,0,0.15)) drop-shadow(1px 1px 3px rgba(0,0,0,0.1));
		pointer-events: auto;
		cursor: grab;
		touch-action: none;
		user-select: none;
		transition: filter 0.2s ease, scale 0.2s ease, opacity 0.2s ease;
	}

	.sticker:hover {
		scale: 1.08;
	}

	.sticker.dragging {
		cursor: grabbing;
		scale: 1;
		opacity: 0.8;
		filter: drop-shadow(6px 12px 24px rgba(0,0,0,0.25)) drop-shadow(3px 6px 12px rgba(0,0,0,0.15));
	}

	/* Juice stickers — clustered toward the left */
	.juice-grid .sticker.s1 { width: 120px; bottom: -30px; left: 10px; transform: rotate(12.5deg); }
	.juice-grid .sticker.s2 { width: 70px; bottom: -15px; left: 100px; transform: rotate(20.7deg); }
	.juice-grid .sticker.s3 { width: 110px; bottom: -35px; left: 170px; transform: rotate(-11.3deg); }
	.juice-grid .sticker.s4 { width: 70px; bottom: -20px; left: 270px; transform: rotate(-14.5deg); }

	/* Daydream stickers — on the right side, slightly larger, clustered together */
	.daydream-grid .sticker.s1 { width: 140px; bottom: 0px; right: -10px; left: auto; transform: rotate(-10deg); }
	.daydream-grid .sticker.s2 { width: 100px; bottom: -20px; right: 130px; left: auto; transform: rotate(15deg); }
	.daydream-grid .sticker.s3 { width: 130px; bottom: -30px; right: 220px; left: auto; transform: rotate(-8deg); }

	/* Photo row below open space */
	.event-photo-row {
		display: flex;
		border-top: var(--b) solid #000;
	}

	.row-photo {
		flex: 1;
		overflow: hidden;
		position: relative;
	}

	.row-photo + .row-photo {
		border-left: var(--b) solid #000;
	}

	.row-photo img {
		width: 100%;
		height: 156px;
		object-fit: cover;
		display: block;
	}

	.row-photo::after {
		content: '';
		position: absolute;
		inset: 0;
		box-shadow: inset 0 0 25px rgba(255,255,255,0.5);
		pointer-events: none;
	}

	/* Gradients on the text/video area only */
	.juice-grid .event-open-space {
		background: linear-gradient(to top, rgba(152,233,151,0.2) 0%, rgba(152,233,151,0) 80%);
	}

	.daydream-grid .event-open-space {
		background: linear-gradient(to top, rgba(255,137,200,0.2) 0%, rgba(255,137,200,0) 80%);
	}

	/* ===== MARQUEE ===== */
	.marquee-section {
		position: relative;
		overflow: visible;
		border-top: var(--b) solid #000;
		border-bottom: var(--b) solid #000;
		margin-top: calc(-1 * var(--b));
		height: 150px;
	}

	.marquee-clip {
		position: relative;
		width: 100%;
		height: 100%;
		overflow: hidden;
		display: flex;
		align-items: center;
	}

	/* Lines extending to page edges */
	.marquee-line-left,
	.marquee-line-right {
		position: absolute;
		top: 50%;
		width: 162px;
		height: var(--b);
		z-index: 3;
	}

	.marquee-line-left {
		right: 100%;
		background: linear-gradient(90deg, transparent, #000);
	}

	.marquee-line-right {
		left: 100%;
		background: linear-gradient(-90deg, transparent, #000);
	}

	.marquee-track {
		display: flex;
		gap: 0.3em;
		white-space: nowrap;
		animation: marquee-scroll 120s linear infinite;
	}

	.marquee-track.reverse {
		animation-direction: reverse;
	}

	.marquee-word {
		font-size: 22px;
		opacity: 0.6;
		flex-shrink: 0;
	}

	.marquee-fade {
		position: absolute;
		top: 0;
		bottom: 0;
		width: 160px;
		z-index: 2;
		pointer-events: none;
	}

	.marquee-fade.left {
		left: 0;
		background: linear-gradient(90deg, #fff 20%, transparent);
	}

	.marquee-fade.right {
		right: 0;
		background: linear-gradient(-90deg, #fff 20%, transparent);
	}

	@keyframes marquee-scroll {
		from { transform: translateX(0); }
		to { transform: translateX(-33.33%); }
	}

	/* ===== THREE-COLUMN EVENTS ===== */
	.three-col-grid {
		display: grid;
		grid-template-columns: 1fr var(--b) 1fr var(--b) 1fr;
	}

	.col-divider-v { background: #000; }

	.three-col-cell {
		position: relative;
		overflow: hidden;
	}

	.col-inner {
		position: relative;
		z-index: 1;
		padding: 24px 20px 40px;
	}

	.col-tint {
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		height: 65%;
		pointer-events: none;
	}

	.col-tint.lavender { background: linear-gradient(to top, rgba(182,172,221,0.2), transparent); }
	.col-tint.cyan { background: linear-gradient(to top, rgba(174,253,254,0.2), transparent); }
	.col-tint.orange { background: linear-gradient(to top, rgba(240,169,90,0.2), transparent); }

	.col-thumb {
		margin-bottom: 20px;
	}

	.col-thumb img {
		width: 100%;
		height: auto;
		aspect-ratio: 16/9;
	}

	.col-title {
		font-family: 'Zarathustra', Georgia, serif;
		font-size: 50px;
		font-weight: 400;
		margin-bottom: 12px;
		text-align: center;
		display: flex;
		align-items: center;
		justify-content: center;
		min-height: 2.4em;
	}

	.col-desc {
		font-size: 22px;
		line-height: 1.4;
	}

	/* ===== FULL-WIDTH GAMES SECTION ===== */
	.games-full-section {
		padding: 24px 0;
		position: relative;
	}

	.games-full-section::before {
		content: '';
		position: absolute;
		inset: 0;
		background: url('/images/pattern.webp') repeat;
		background-size: 40px 40px;
		opacity: 0.03;
		pointer-events: none;
	}

	.games-heading-area {
		position: relative;
		text-align: center;
		padding: 120px 40px 60px;
		border-top: var(--b) solid #000;
		margin-top: calc(-1 * var(--b));
	}

	.games-heading-glow {
		position: absolute;
		inset: 0;
		pointer-events: none;
		background: linear-gradient(to top, rgba(var(--glow-r), var(--glow-g), var(--glow-b), 0.1), transparent);
		transition: --glow-r 0.5s ease, --glow-g 0.5s ease, --glow-b 0.5s ease;
	}

	.games-heading-area::before,
	.games-heading-area::after {
		content: '';
		position: absolute;
		top: 0;
		bottom: 0;
		width: 100vw;
		pointer-events: none;
		background: linear-gradient(to top, rgba(17, 15, 35, 0.1), transparent);
		z-index: 1;
	}
	.games-heading-area::before { right: 100%; }
	.games-heading-area::after { left: 100%; }

	.games-heading {
		position: relative;
		font-family: 'Zarathustra', Georgia, serif;
		font-size: 50px;
		font-weight: 400;
		margin-bottom: 12px;
	}

	.games-sub {
		position: relative;
		font-size: 24px;
		opacity: 0.6;
	}

	.games-showcase {
		position: relative;
		overflow: visible;
		border-top: var(--b) solid #000;
		border-bottom: var(--b) solid #000;
		background: #fff;
	}

	.games-carousel {
		position: relative;
		width: 1232px;
		height: 566px;
		margin: 0 auto;
		z-index: 1;
		overflow: visible;
	}

	.games-carousel.animating {
		overflow: visible;
	}

	.side-card {
		width: 120px;
		border-left: var(--b) solid #000;
		border-right: var(--b) solid #000;
		display: flex;
		flex-direction: column;
		align-items: center;
		overflow: hidden;
	}

	.side-thumb-wrap {
		width: 76px;
		height: 76px;
		border: var(--b) solid #000;
		overflow: hidden;
		margin-top: 20px;
		flex-shrink: 0;
	}

	.side-thumb-wrap img { width: 100%; height: 100%; object-fit: cover; }

	.side-hline {
		width: 100%;
		height: var(--b);
		background: #000;
		margin-top: 22px;
		flex-shrink: 0;
		position: relative;
	}

	.side-hline::before,
	.side-hline::after {
		content: '';
		position: absolute;
		width: 9px;
		height: 9px;
		background: #000;
		top: -4px;
	}
	.side-hline::before { left: -4px; }
	.side-hline::after { right: -4px; }

	.side-bars {
		display: flex;
		gap: 24px;
		padding: 0;
		margin-top: auto;
	}

	.side-vbar {
		width: var(--b);
		height: 80px;
		background: #000;
		position: relative;
	}

	.side-vbar::after {
		content: '';
		position: absolute;
		bottom: -4px;
		left: -4px;
		width: 9px;
		height: 9px;
		background: #000;
	}

	.main-game-card {
		width: 560px;
		border-left: var(--b) solid #000;
		border-right: var(--b) solid #000;
		position: relative;
		overflow: visible;
		display: flex;
		flex-direction: column;
	}

	.game-cover { border-bottom: var(--b) solid #000; flex-shrink: 0; }

	.game-cover img {
		width: 100%;
		height: 260px;
		object-fit: cover;
		display: block;
	}

	.game-meta-area {
		padding: 20px 24px 32px;
		border-bottom: var(--b) solid #000;
		flex: 1;
		min-height: 0;
	}

	.game-name {
		font-family: 'Phantom Sans', sans-serif;
		font-size: 38px;
		font-weight: 700;
		margin-bottom: 4px;
	}

	.game-byline {
		display: flex;
		align-items: center;
		gap: 12px;
		font-size: 24px;
		margin-bottom: 10px;
	}

	.meta-dot { font-size: 22px; }
	.faded { opacity: 0.5; }

	.game-description {
		font-size: 24px;
		line-height: 1.45;
		height: 70px;
		overflow: hidden;
	}

	.game-nav {
		display: flex;
		height: 82px;
		flex-shrink: 0;
	}

	.nav-cell {
		display: flex;
		align-items: center;
		justify-content: center;
		border: none;
		border-right: var(--b) solid #000;
		background: #fff;
		cursor: pointer;
		padding: 0;
		transition: background 0.15s, color 0.15s;
	}

	.nav-cell:hover { background: #000; }
	.nav-cell:hover svg path { stroke: #fff; fill: none; }
	.nav-play-cell:hover svg path { fill: #fff; stroke: none; }

	.nav-cell:last-child { border-right: none; }

	.nav-arrow-cell { width: 118px; flex-shrink: 0; }
	.nav-play-cell { flex: 1; }

	.nav-cell img, .nav-cell svg { width: 28px; height: 28px; object-fit: contain; }
	.nav-cell svg path { transition: stroke 0.15s, fill 0.15s; }

	/* ===== CAROUSEL ANIMATIONS ===== */

	/* Edge cards tracking fold/unfold — sine easing matches rotateY's cos(θ) projection */
	/* "unfold" = adjacent to the NEW face appearing (ease-out-sine: fast start, slow finish = sin curve) */
	/* "fold" = adjacent to the OLD face disappearing (ease-in-sine: slow start, fast finish = 1-cos curve) */
	.edge-unfold-left { animation: edge-left 350ms cubic-bezier(0.61, 1, 0.88, 1) forwards; }
	.edge-unfold-right { animation: edge-right 350ms cubic-bezier(0.61, 1, 0.88, 1) forwards; }
	.edge-fold-left { animation: edge-left 350ms cubic-bezier(0.12, 0, 0.39, 0) forwards; }
	.edge-fold-right { animation: edge-right 350ms cubic-bezier(0.12, 0, 0.39, 0) forwards; }
	/* Exit/enter variants — travel further (200px) with fade */
	.edge-exit-unfold-left { animation: edge-far-left 350ms cubic-bezier(0.61, 1, 0.88, 1) forwards, fade-out 350ms linear forwards; }
	.edge-exit-unfold-right { animation: edge-far-right 350ms cubic-bezier(0.61, 1, 0.88, 1) forwards, fade-out 350ms linear forwards; }
	.edge-enter-fold-left { animation: edge-far-left 350ms cubic-bezier(0.12, 0, 0.39, 0) forwards, fade-in 350ms linear forwards; }
	.edge-enter-fold-right { animation: edge-far-right 350ms cubic-bezier(0.12, 0, 0.39, 0) forwards, fade-in 350ms linear forwards; }

	/* Outer edge card staggers after inner edge card */
	.edge-outer { animation-delay: 80ms; animation-fill-mode: both; }
	.anim-delayed.edge-outer { animation-delay: 200ms; }

	/* Flip pair: zero-width hinge with 3D perspective */
	.flip-pair {
		width: 0;
		overflow: visible;
		perspective: 120000px;
		transform-style: preserve-3d;
	}

	.anim-flip-slide-left { animation: flip-slide-left 350ms cubic-bezier(0.05, 0.8, 0.15, 1) forwards; }
	.anim-flip-slide-right { animation: flip-slide-right 350ms cubic-bezier(0.05, 0.8, 0.15, 1) forwards; }

	/* Navigate Right: hinge on left, old folds away CW, new unfolds CW */
	.flip-old-nr { transform-origin: left center; animation: fold-out-cw 350ms linear forwards; backface-visibility: hidden; }
	.flip-new-nr { transform-origin: right center; animation: fold-in-cw 350ms linear forwards; backface-visibility: hidden; }

	/* Navigate Left: hinge on right, old folds away CCW, new unfolds CCW */
	.flip-old-nl { transform-origin: right center; animation: fold-out-ccw 350ms linear forwards; backface-visibility: hidden; }
	.flip-new-nl { transform-origin: left center; animation: fold-in-ccw 350ms linear forwards; backface-visibility: hidden; }

	/* Second-wave delay: incoming game waits for outgoing to mostly finish */
	.anim-delayed { animation-delay: 120ms; animation-fill-mode: both; }

	/* 3D rotation keyframes — perspective() handled by parent */
	@keyframes fold-out-cw { from { transform: rotateY(0deg); } to { transform: rotateY(90deg); } }
	@keyframes fold-in-cw { from { transform: rotateY(-90deg); } to { transform: rotateY(0deg); } }
	@keyframes fold-out-ccw { from { transform: rotateY(0deg); } to { transform: rotateY(-90deg); } }
	@keyframes fold-in-ccw { from { transform: rotateY(90deg); } to { transform: rotateY(0deg); } }

	/* Gradient shadow overlay — darker on the far edge, transparent near the hinge */
	.flip-old-nr::after, .flip-new-nr::after,
	.flip-old-nl::after, .flip-new-nl::after {
		content: '';
		position: absolute;
		inset: 0;
		pointer-events: none;
		z-index: 10;
	}

	/* Navigate Right: hinge on left */
	.flip-old-nr::after { background: linear-gradient(to right, transparent, rgba(0,0,0,0.12)); animation: shade-in 350ms linear forwards; }
	.flip-new-nr::after { background: linear-gradient(to left, transparent, rgba(0,0,0,0.12)); animation: shade-out 350ms linear forwards; }

	/* Navigate Left: hinge on right */
	.flip-old-nl::after { background: linear-gradient(to left, transparent, rgba(0,0,0,0.12)); animation: shade-in 350ms linear forwards; }
	.flip-new-nl::after { background: linear-gradient(to right, transparent, rgba(0,0,0,0.12)); animation: shade-out 350ms linear forwards; }

	/* Delayed flip faces need delayed shading too */
	.anim-delayed::after { animation-delay: 120ms; animation-fill-mode: both; }

	@keyframes shade-in { from { opacity: 0; } to { opacity: 1; } }
	@keyframes shade-out { from { opacity: 1; } to { opacity: 0; } }

	/* Slide keyframes */
	@keyframes flip-slide-left { from { transform: translateX(0); } to { transform: translateX(-48px); } }
	@keyframes flip-slide-right { from { transform: translateX(0); } to { transform: translateX(48px); } }
	@keyframes edge-left { from { transform: translateX(0); } to { transform: translateX(-120px); } }
	@keyframes edge-right { from { transform: translateX(0); } to { transform: translateX(120px); } }
	@keyframes edge-far-left { from { transform: translateX(0); } to { transform: translateX(-200px); } }
	@keyframes edge-far-right { from { transform: translateX(0); } to { transform: translateX(200px); } }
	@keyframes fade-out { from { opacity: 1; } to { opacity: 0; } }
	@keyframes fade-in { from { opacity: 0; } to { opacity: 1; } }

	/* ===== DONATE BORDERED WRAPPER ===== */
	.donate-bordered-wrapper {
		position: relative;
		max-width: 1440px;
		margin: 0 auto;
	}

	.donate-bordered-wrapper::before {
		content: '';
		position: absolute;
		top: 0;
		left: 50%;
		transform: translateX(-50%);
		width: 100vw;
		height: var(--b);
		background: #000;
		z-index: 4;
	}

	/* ===== DONATE ===== */
	.donate-section {
		position: relative;
		margin: 0 162px;
		z-index: 2;
	}

	.donate-heading-area {
		position: relative;
		padding: 120px 40px 60px;
		text-align: center;
	}

	.donate-heading-glow {
		position: absolute;
		inset: 0;
		pointer-events: none;
		background: linear-gradient(to bottom, rgba(var(--glow-r), var(--glow-g), var(--glow-b), 0.1), transparent);
		transition: --glow-r 0.5s ease, --glow-g 0.5s ease, --glow-b 0.5s ease;
	}

	.donate-heading-area::before,
	.donate-heading-area::after {
		content: '';
		position: absolute;
		top: 0;
		bottom: 0;
		width: 100vw;
		pointer-events: none;
		background: linear-gradient(to bottom, rgba(17, 15, 35, 0.1), transparent);
		z-index: 1;
	}
	.donate-heading-area::before { right: 100%; }
	.donate-heading-area::after { left: 100%; }

	.donate-heading {
		position: relative;
		font-family: 'Zarathustra', Georgia, serif;
		font-size: 50px;
		font-weight: 400;
		line-height: 1.2;
	}

	.donate-columns {
		display: grid;
		grid-template-columns: 1fr var(--b) 1fr;
		border-top: var(--b) solid #000;
		border-bottom: var(--b) solid #000;
	}

	.donate-divider { background: #000; }

	.donate-col {
		position: relative;
		overflow: hidden;
	}

	.donate-col::before {
		content: '';
		position: absolute;
		inset: 0;
		background: linear-gradient(to top, rgba(80,159,220,0.1) 0%, rgba(80,159,220,0) 80%);
		opacity: 0;
		transition: opacity 0.1s;
		pointer-events: none;
	}

	.donate-col:hover::before {
		opacity: 1;
	}

	.donate-col-pattern {
		position: absolute;
		inset: 0;
		background:
			linear-gradient(0deg, rgba(255,255,255,0) 0%, rgba(255,255,255,1) 100%),
			url('/images/pattern.webp') repeat;
		background-size: auto, 40px 40px;
		opacity: 0.03;
		pointer-events: none;
		transition: opacity 0.1s;
	}

	.donate-col:hover .donate-col-pattern {
		opacity: 0.04;
	}

	.donate-col-inner {
		position: relative;
		z-index: 1;
		padding: 40px 32px;
		display: flex;
		flex-direction: column;
		height: 100%;
	}

	.donate-col-title {
		font-family: 'Zarathustra', Georgia, serif;
		font-size: 36px;
		font-weight: 400;
		text-align: center;
		margin-bottom: 24px;
	}

	.donate-col-body {
		font-size: 20px;
		line-height: 1.5;
		margin-bottom: 24px;
	}

	.donate-col-body p { margin-bottom: 16px; }

	.donate-btn {
		margin: auto auto 0;
		background: #fff;
	}

	/* ===== LOGO STRIP ===== */
	.logo-strip {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		margin: 0 162px;
		position: relative;
		z-index: 2;
	}

	.logo-cell {
		aspect-ratio: 1;
		border-right: var(--b) solid #000;
		position: relative;
		overflow: hidden;
	}

	.logo-cell::before {
		content: '';
		position: absolute;
		inset: 0;
		background: linear-gradient(to top, rgba(var(--cell-r-g-b), 0.15) 0%, rgba(var(--cell-r-g-b), 0) 80%);
		opacity: 0;
		pointer-events: none;
	}

	.logo-cell:global(.flash)::before {
		animation: cell-flash 0.6s ease-out forwards;
	}

	.logo-cell:last-child { border-right: none; }

	.logo-cell-pattern {
		position: absolute;
		inset: 0;
		background-size: auto, 40px 40px;
		opacity: 0;
		pointer-events: none;
	}

	.logo-cell:global(.flash) .logo-cell-pattern {
		animation: pattern-flash 0.6s ease-out forwards;
	}

	@keyframes cell-flash {
		0% { opacity: 0; }
		15% { opacity: 1; }
		100% { opacity: 0; }
	}

	@keyframes pattern-flash {
		0% { opacity: 0; }
		15% { opacity: 0.06; }
		100% { opacity: 0; }
	}

	/* ===== FOOTER ===== */
	.footer {
		background: #000;
		color: #fff;
		overflow: hidden;
	}

	.footer-black-line { height: var(--b); background: #000; }
	.footer-white-line { height: 4px; background: #fff; }

	.footer-top {
		text-align: center;
		padding: 70px 40px 24px;
	}

	.footer-tagline { font-size: 22px; margin-bottom: 12px; }

	.footer-links {
		display: flex;
		justify-content: center;
		align-items: center;
		gap: 18px;
	}

	.footer-links a { text-decoration: underline; font-size: 22px; }
	.footer-dot { opacity: 0.5; font-size: 32px; }

	.footer-credit {
		font-size: 22px;
		opacity: 0.5;
		margin-top: 16px;
	}

	.footer-credit a {
		text-decoration: underline;
	}

	.footer-tile {
		height: 200px;
		margin-top: 40px;
		background: url('/images/footer-tile.webp') repeat-x;
		background-size: auto 100%;
		background-position: center bottom;
	}

	/* ===== RESPONSIVE ===== */
	/* Push hero images outward when viewport makes them crowd the hero text */
	@media (max-width: 1500px) and (min-width: 769px) {
		.g1, .g2, .g3, .g4, .g9, .g10, .g13, .g14, .g15, .g19, .g21, .g22 {
			translate: -60px 0;
		}
		.g5, .g6, .g7, .g8, .g11, .g12, .g16, .g17, .g18, .g20, .g23 {
			translate: 60px 0;
		}
	}

	@media (max-width: 1200px) {
		.bordered-content { margin: 0 60px; }
		.donate-section { margin: 0 60px; }
		.logo-strip { margin: 0 60px; }
		.left-pattern { right: calc(100% - 60px); }
		.right-pattern { left: calc(100% - 60px); }
		.border-line.left-line { left: 60px; }
		.border-line.right-line { right: 60px; }
		.dot-top-left, .dot-bottom-left { left: 56px; }
		.dot-top-right, .dot-bottom-right { right: 56px; }
		.marquee-line-left, .marquee-line-right { width: 60px; }
		.about-blurb { margin: 0 60px; padding: 48px 40px; }
		.hero { height: auto; min-height: 600px; padding: 200px 20px 20px; max-height: none; }
		.hero-heading-top { font-size: 36px; }
		.hero-heading-big { font-size: 64px; }
		.hero-join { font-size: 14px; }

		/* Top images — nudge up */
		.g21 { top: -200px; }
		.g22 { top: -210px; }
		.g23 { top: -195px; }
		.g4  { top: -120px; }
		.g5  { top: -130px; }
		.g2  { top: -70px; }
		.g7  { top: -70px; }

		/* Bottom row — nudge down */
		.g13 { bottom: -50px; }
		.g14 { bottom: -100px; }
		.g15 { bottom: -90px; }
		.g16 { bottom: -50px; }
		.g17 { bottom: -100px; }
		.g18 { bottom: -90px; }

		.juice-grid, .daydream-grid { grid-template-columns: 1fr; }
		.grid-divider { height: var(--b); }
		.photo-stack { max-height: 400px; }

		.event-title { font-size: 42px; }
		.event-desc { font-size: 18px; }
		.video-thumb img, .video-thumb iframe { width: 280px; height: 160px; }
		.marquee-section { height: auto; }
		.marquee-clip { padding: 20px 0; }

		.three-col-section { margin-left: -60px; margin-right: -60px; }
		.three-col-grid { grid-template-columns: 1fr; }
		.col-divider-v { height: var(--b); width: 100%; }
		.col-inner { padding: 24px 60px 32px; text-align: center; }
		.col-thumb { max-width: 500px; margin-left: auto; margin-right: auto; }
		.col-desc { font-size: 18px; max-width: 500px; margin-left: auto; margin-right: auto; }
		.col-title { font-size: 36px; }

		.games-carousel { width: auto; height: auto; display: flex; justify-content: center; }
		.side-card { display: none !important; }
		.main-game-card { position: relative !important; left: auto !important; top: auto !important; bottom: auto !important; width: 100% !important; max-width: 600px; }
		.game-cover img { height: 300px; }
		.game-meta-area { height: auto; }
		.game-name { font-size: 36px; }
		.game-byline, .game-description { font-size: 18px; }

		.games-heading { font-size: 42px; }
		.games-sub { font-size: 22px; }
		.donate-heading { font-size: 42px; }
		.donate-columns { grid-template-columns: 1fr; }
		.donate-divider { height: var(--b); }
		.donate-col-title { font-size: 32px; }
		.donate-col-body { font-size: 18px; }
		.donate-col { min-height: auto; }

		.logo-strip { grid-template-columns: repeat(4, 1fr); }

		.footer-top { padding: 48px 40px 32px; }
		.footer-tagline { font-size: 22px; }
		.footer-links a { font-size: 22px; }
	}

	@media (max-width: 768px) {
		/* Margins & decorative elements — 10px margins with border lines + patterns */
		.bordered-content { margin: 0 10px; }
		.donate-section { margin: 0 10px; }
		.logo-strip { margin: 0 10px; }
		.left-pattern { right: calc(100% - 10px); }
		.right-pattern { left: calc(100% - 10px); }
		.border-line.left-line { left: 10px; }
		.border-line.right-line { right: 10px; }
		.dot-top-left, .dot-bottom-left { left: 6px; }
		.dot-top-right, .dot-bottom-right { right: 6px; }
		.marquee-line-left, .marquee-line-right { width: 10px; }
		.games-heading-area::before, .games-heading-area::after,
		.donate-heading-area::before, .donate-heading-area::after { display: none; }

		/* About blurb */
		.about-blurb { margin: 0; padding: 32px 20px; font-size: 16px; }

		/* Hero */
		.hero { height: 100svh; min-height: 0; max-height: none; padding: 0 20px; }
		.hero-content { justify-content: center; padding-bottom: 0; }
		.hero-heading-top { font-size: 26px; }
		.hero-heading-big { font-size: 44px; }
		.hero-join { font-size: 14px; }
		.btn-pill { width: 160px; height: 48px; font-size: 16px; }

		/* Mobile game images */
		.game-shot {
			width: 160px;
			height: 120px;
			border: 3px solid #fff;
		}
		/* Hide desktop positions, use mobile layout */
		.g1, .g2, .g3, .g4, .g5, .g6, .g7, .g8, .g9, .g10, .g11, .g12,
		.g19, .g20, .g21, .g22, .g23 { display: none; }

		/* Bottom-left — slope outward going up */
		.g13 { display: block; left: -30px;  bottom: -30px;  transform: rotate(5deg);  }
		.g14 { display: block; left: -70px;  bottom: 70px;   transform: rotate(-3deg); }
		.g15 { display: block; left: -110px; bottom: 170px;  transform: rotate(4deg);  }
		/* Bottom-right — slope outward going up */
		.g16 { display: block; right: -30px; bottom: -30px;  transform: rotate(-4deg); }
		.g17 { display: block; right: -70px; bottom: 70px;   transform: rotate(6deg);  }
		.g18 { display: block; right: -110px;bottom: 170px;  transform: rotate(-3deg); }
		/* Come back in at top */
		.g21 { display: block; left: -40px;  top: -40px;  transform: rotate(-6deg); }
		.g22 { display: block; left: 100px;  top: -60px;  transform: rotate(3deg);  }
		.g23 { display: block; right: -40px; top: -40px;  transform: rotate(5deg);  }

		/* Juice/Daydream reorder — text+video first */
		.juice-grid .event-right-col { order: 0; }
		.juice-grid .grid-divider { order: 1; }
		.juice-grid .photo-stack { order: 2; }

		.event-columns { flex-direction: column; }
		.daydream-columns { flex-direction: column; }
		.video-thumb img, .video-thumb iframe { width: 100%; height: auto; }
		.sticker-cluster { display: none; }

		.event-photo-row { flex-wrap: wrap; }
		.row-photo { min-width: 50%; }
		.row-photo img { height: 120px; }

		/* Marquee — more vertical padding, smaller fade gradients */
		.marquee-clip { padding: 28px 0; }
		.marquee-fade { width: 60px; }

		/* Three-col events */
		.three-col-section { margin-left: -10px; margin-right: -10px; }
		.col-inner { padding: 16px 24px 24px; }
		.col-title { font-size: 32px; }
		.col-desc { font-size: 16px; }
		.col-thumb img { width: 100%; }

		/* Games heading — larger font, less padding */
		.games-heading { font-size: 38px; }
		.games-heading-area { padding: 72px 20px 40px; }
		.games-sub { font-size: 16px; }
		.game-nav { height: 70px; }
		.nav-arrow-cell { width: 80px; }

		/* Donate */
		.donate-heading { font-size: 36px; }
		.donate-col-inner { padding: 32px 24px; }
		.donate-col-title { font-size: 26px; }
		.donate-col-body { font-size: 16px; }

		/* Footer — normalized font sizes */
		.footer-top { padding: 32px 20px 20px; }
		.footer-tagline { font-size: 16px; }
		.footer-links a { font-size: 15px; }
		.footer-links { gap: 10px; flex-wrap: wrap; justify-content: center; }
		.footer-dot { font-size: 20px; }
		.footer-credit { font-size: 14px; margin-top: 12px; }
		.footer-tile { height: 100px; margin-top: 16px; }

		/* Logo strip — 5 squares, hide indigo + violet */
		.logo-strip { grid-template-columns: repeat(5, 1fr); }
		.logo-cell:nth-child(n+6) { display: none; }
	}
</style>
