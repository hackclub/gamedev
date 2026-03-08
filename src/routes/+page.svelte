<script lang="ts">
	let currentGame = $state(0);
</script>

<!-- HERO SECTION -->
<section class="hero">
	<div class="hero-pattern"></div>
	<div class="hero-games">
		<img src="/images/hero-game-7.png" alt="" class="game-shot g1" />
		<img src="/images/hero-game-8.png" alt="" class="game-shot g2" />
		<img src="/images/hero-game-9.png" alt="" class="game-shot g3" />
		<img src="/images/hero-game-11.png" alt="" class="game-shot g4" />
		<img src="/images/hero-game-12.png" alt="" class="game-shot g5" />
		<img src="/images/hero-game-1.png" alt="" class="game-shot g6" />
		<img src="/images/hero-game-2.png" alt="" class="game-shot g7" />
		<img src="/images/hero-game-5.png" alt="" class="game-shot g8" />
		<img src="/images/hero-game-6.png" alt="" class="game-shot g9" />
		<img src="/images/hero-game-3.png" alt="" class="game-shot g10" />
		<img src="/images/hero-game-10.png" alt="" class="game-shot g11" />
		<img src="/images/hero-game-4.png" alt="" class="game-shot g12" />
		<img src="/images/hero-game-1.png" alt="" class="game-shot g13" />
		<img src="/images/hero-game-5.png" alt="" class="game-shot g14" />
		<img src="/images/hero-game-9.png" alt="" class="game-shot g15" />
		<img src="/images/hero-game-3.png" alt="" class="game-shot g16" />
		<img src="/images/hero-game-6.png" alt="" class="game-shot g17" />
		<img src="/images/hero-game-11.png" alt="" class="game-shot g18" />
		<img src="/images/hero-game-2.png" alt="" class="game-shot g19" />
		<img src="/images/hero-game-4.png" alt="" class="game-shot g20" />
	</div>
	<div class="hero-vignette"></div>
	<div class="hero-content">
		<p class="hero-heading-top">
			Hack Club is where <span class="underlined">high schoolers</span><br />
			go from playing games
		</p>
		<h1 class="hero-heading-big">to making games.</h1>
		<div class="hero-cta">
			<a href="#donate" class="btn-pill">Donate</a>
		</div>
		<p class="hero-join">Teenager? Join Hack Club!</p>
		<div class="hero-arrow">
			<svg width="40" height="24" viewBox="0 0 40 24" fill="none">
				<path d="M2 2L20 20L38 2" stroke="#ec3750" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
			</svg>
		</div>
	</div>
</section>

<!-- SUBHEADER TEXT -->
<div class="subheader">
	<p>Our flagship hackathons CHANGE THIS CHANGE THIS — maybe we should write here the line about being a global movement 501c3 nonprofit</p>
</div>

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

	<div class="bordered-content">

		<!-- ====== JUICE SECTION ====== -->
		<section class="event-section">
			<div class="juice-gradient"></div>
			<div class="event-grid juice-grid">
				<!-- LEFT: Two stacked photos -->
				<div class="photo-stack">
					<div class="stack-photo"><img src="/images/juice-1.png" alt="Juice group photo" /></div>
					<div class="stack-photo"><img src="/images/juice-2.png" alt="Juice whiteboard" /></div>
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
									<img src="/images/juice-video-thumb.png" alt="Juice video" />
								</div>
								<span class="watch-label">watch the video <span class="watch-arrow">↗</span></span>
							</div>
						</div>
						<!-- Stickers cluster -->
						<div class="sticker-cluster">
							<img src="/images/sticker-holo-1.png" alt="" class="sticker s1" />
							<img src="/images/sticker-1.png" alt="" class="sticker s2" />
							<img src="/images/sticker-2.png" alt="" class="sticker s3" />
							<img src="/images/sticker-3-holo.png" alt="" class="sticker s4" />
						</div>
					</div>
					<div class="event-photo-row">
						<div class="row-photo"><img src="/images/juice-3.png" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-4.png" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-5.png" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-6.png" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-7.png" alt="" /></div>
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
			<div class="daydream-gradient"></div>
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
									<img src="/images/daydream-video-thumb.png" alt="Daydream video" />
								</div>
								<span class="watch-label">watch the video <span class="watch-arrow">↗</span></span>
							</div>
						</div>
						<div class="sticker-cluster">
							<img src="/images/sticker-holo-1.png" alt="" class="sticker s1" />
							<img src="/images/sticker-2.png" alt="" class="sticker s2" />
							<img src="/images/sticker-3-holo.png" alt="" class="sticker s3" />
						</div>
					</div>
					<div class="event-photo-row">
						<div class="row-photo"><img src="/images/juice-3.png" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-4.png" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-5.png" alt="" /></div>
						<div class="row-photo"><img src="/images/juice-8.png" alt="" /></div>
					</div>
				</div>
				<!-- Vertical divider -->
				<div class="grid-divider">
					<div class="line-dot" style="top:-4px;left:-4px;"></div>
					<div class="line-dot" style="bottom:-4px;left:-4px;"></div>
				</div>
				<!-- RIGHT: Two stacked photos -->
				<div class="photo-stack">
					<div class="stack-photo"><img src="/images/daydream-photo.png" alt="Daydream group photo" /></div>
					<div class="stack-photo"><img src="/images/juice-2.png" alt="Daydream whiteboard" /></div>
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
							<img src="/images/juice-video-thumb.png" alt="Campfire Flagship" />
						</div>
						<h3 class="col-title">Campfire Flagship</h3>
						<p class="col-desc">uhhhh</p>
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
							<img src="/images/juice-video-thumb.png" alt="Overglade" />
						</div>
						<h3 class="col-title">Overglade</h3>
						<p class="col-desc">blah blah blah blah<br/>blah blah blah blah<br/>blah blah blah blah blah</p>
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
							<img src="/images/juice-video-thumb.png" alt="Campfire" />
						</div>
						<h3 class="col-title">Campfire</h3>
						<p class="col-desc">blah blah blah blah<br/>blah blah blah blah<br/>blah blah blah blah blah</p>
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
			<h2 class="games-heading">Real games built by teenagers</h2>
			<p class="games-sub">Don't take our word for it — see for yourself.</p>
		</div>

		<!-- GAMES SHOWCASE (inside bordered area) -->
		<section class="games-showcase">
			<div class="games-pattern-strip top"></div>
			<div class="games-pattern-strip bottom"></div>
			<div class="games-carousel">
				<div class="side-card blue-tint">
					<div class="side-thumb-wrap"><img src="/images/game-side-thumb.png" alt="" /></div>
					<div class="side-hline"></div>
					<div class="side-bars">
						<div class="side-vbar"></div>
						<div class="side-vbar"></div>
						<div class="side-vbar"></div>
					</div>
				</div>
				<div class="side-card purple-tint">
					<div class="side-thumb-wrap"><img src="/images/game-side-thumb.png" alt="" /></div>
					<div class="side-hline"></div>
					<div class="side-bars">
						<div class="side-vbar"></div>
						<div class="side-vbar"></div>
						<div class="side-vbar"></div>
					</div>
				</div>

				<div class="main-game-card">
					<div class="corner-dot tl"></div>
					<div class="corner-dot tr"></div>
					<div class="corner-dot bl"></div>
					<div class="corner-dot br"></div>
					<div class="game-cover">
						<img src="/images/prode-dies.png" alt="prode dies" />
					</div>
					<div class="game-meta-area">
						<h3 class="game-name">prode dies</h3>
						<div class="game-byline">
							<span>By Herby, 17</span>
							<span class="meta-dot">·</span>
							<span class="faded">from Canada</span>
						</div>
						<p class="game-description">A visual novel about a teenager trying to solve their own murder.</p>
					</div>
					<div class="game-nav">
						<button class="nav-cell nav-arrow-cell"><img src="/images/arrow-left.png" alt="Previous" /></button>
						<button class="nav-cell nav-play-cell"><img src="/images/play-icon.png" alt="Play" class="play-icon" /></button>
						<button class="nav-cell nav-arrow-cell"><img src="/images/arrow-right.png" alt="Next" /></button>
					</div>
				</div>

				<div class="side-card purple-tint">
					<div class="side-thumb-wrap"><img src="/images/game-side-thumb.png" alt="" /></div>
					<div class="side-hline"></div>
					<div class="side-bars">
						<div class="side-vbar"></div>
						<div class="side-vbar"></div>
						<div class="side-vbar"></div>
					</div>
				</div>
				<div class="side-card blue-tint">
					<div class="side-thumb-wrap"><img src="/images/game-side-thumb.png" alt="" /></div>
					<div class="side-hline"></div>
					<div class="side-bars">
						<div class="side-vbar"></div>
						<div class="side-vbar"></div>
						<div class="side-vbar"></div>
					</div>
				</div>
			</div>
		</section>
	</div>

	<!-- Dot at bottom of lines -->
	<div class="line-dot dot-bottom-left"></div>
	<div class="line-dot dot-bottom-right"></div>
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
			<h2 class="donate-heading">Help a high schooler become<br/>a game developer</h2>
		</div>
		<div class="donate-columns">
			<div class="donate-col">
				<div class="donate-col-pattern"></div>
				<div class="donate-col-inner">
					<h3 class="donate-col-title">Contribute financially</h3>
					<div class="donate-col-body">
						<p>Everything you donate will go directly into gamedev events.</p>
						<p>$100 = a Steam license to publish a video game<br/>
						$500 = 1 ticket to a flagship hackathon<br/>
						$650 = 1 ticket + round-trip ground transportation to a flagship hackathon<br/>
						$1500 = 1 ticket + flight to a flagship hackathon</p>
						<p>All donations are 100% tax deductable in the US. Blah blah blah. We believe in full transparency — our finances are publicly available, and you can view them XXXX.</p>
					</div>
					<a href="#" class="btn-pill donate-btn">Donate</a>
				</div>
			</div>
			<div class="donate-divider"></div>
			<div class="donate-col">
				<div class="donate-col-pattern"></div>
				<div class="donate-col-inner">
					<h3 class="donate-col-title">Contribute in other ways</h3>
					<div class="donate-col-body">
						<p>Donate your space — we're running in-person hackathons all over the world, and we'd love to use your space.</p>
						<p>Donate 30 minutes of your time — are you someone cool who kids would be interested in talking to? we'd love to have you for an AMA, or list a 30-minute call with you as a prize!</p>
						<p>Donate your game — do you have a game published on steam? if you donate us bulk steam keys, we'll use it as a reward for making games!</p>
					</div>
					<a href="#" class="btn-pill donate-btn">Donate</a>
				</div>
			</div>
		</div>
	</section>

	<!-- LOGO STRIP -->
	<div class="logo-strip">
		{#each Array(7) as _}
			<div class="logo-cell"></div>
		{/each}
	</div>
</div>

<!-- FOOTER -->
<footer class="footer">
	<div class="footer-black-line"></div>
	<div class="footer-white-line"></div>
	<div class="footer-top">
		<p class="footer-tagline">made with &lt;3 by teenagers, for teenagers</p>
		<nav class="footer-links">
			<a href="https://hackclub.com">Hack Club</a>
			<span class="footer-dot">·</span>
			<a href="https://hackclub.com/slack">Slack</a>
			<span class="footer-dot">·</span>
			<a href="https://hackclub.com/clubs">Clubs</a>
			<span class="footer-dot">·</span>
			<a href="https://hackclub.com/hackathons">Hackathons</a>
		</nav>
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
	}

	.hero-pattern {
		position: absolute;
		inset: 0;
		background: url('/images/pattern.png') repeat;
		background-size: 40px 40px;
		opacity: 0.03;
		transform: rotate(180deg);
		pointer-events: none;
	}

	.hero-games { position: absolute; inset: 0; pointer-events: none; }

	.game-shot {
		position: absolute;
		width: 220px;
		height: 165px;
		border: 3px solid #fff;
		border-radius: 8px;
		object-fit: cover;
	}

	/* Left column – far left */
	.g1  { left: -70px;  top: 60px;   transform: rotate(3deg);    opacity: 0.7; }
	.g2  { left: -60px;  top: 300px;  transform: rotate(15deg);   opacity: 0.85; }
	.g3  { left: -80px;  top: 540px;  transform: rotate(-3deg);   opacity: 0.9; }
	.g4  { left: -60px;  top: 760px;  transform: rotate(2deg);    opacity: 0.95; }
	/* Right column – far right */
	.g5  { right: -70px; top: 60px;   transform: rotate(-13deg);  opacity: 0.6; }
	.g6  { right: -60px; top: 300px;  transform: rotate(-11deg);  opacity: 0.8; }
	.g7  { right: -80px; top: 540px;  transform: rotate(11deg);   opacity: 0.9; }
	.g8  { right: -60px; top: 760px;  transform: rotate(-9deg);   opacity: 0.95; }
	/* Center-left column */
	.g9  { left: 120px;  top: -50px;  transform: rotate(-19deg);  opacity: 0.18; }
	.g10 { left: 150px;  top: 200px;  transform: rotate(7deg);    opacity: 0.14; }
	.g11 { left: 130px;  top: 450px;  transform: rotate(5deg);    opacity: 0.1; }
	/* Center-right column */
	.g12 { right: 120px; top: -50px;  transform: rotate(9deg);    opacity: 0.18; }
	.g13 { right: 150px; top: 200px;  transform: rotate(-6deg);   opacity: 0.14; }
	.g14 { right: 130px; top: 450px;  transform: rotate(-7deg);   opacity: 0.1; }
	/* Bottom scatter */
	.g15 { left: 80px;   bottom: -20px; transform: rotate(9deg);  opacity: 0.9; }
	.g16 { right: 80px;  bottom: -20px; transform: rotate(-8deg); opacity: 0.9; }
	.g17 { left: 350px;  bottom: 30px;  transform: rotate(12deg); opacity: 0.5; }
	.g18 { right: 350px; bottom: 30px;  transform: rotate(-12deg);opacity: 0.5; }
	.g19 { left: 540px;  bottom: -30px; transform: rotate(-2deg); opacity: 0.3; }
	.g20 { right: 540px; bottom: -30px; transform: rotate(3deg);  opacity: 0.3; }

	.hero-vignette {
		position: absolute;
		inset: 0;
		background: radial-gradient(ellipse 55% 50% at 50% 42%, rgba(255,255,255,0.96) 0%, rgba(255,255,255,0.89) 55%, rgba(255,255,255,0) 100%);
		pointer-events: none;
		z-index: 1;
	}

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
		left: 0;
		right: 0;
		bottom: -8px;
		height: 16px;
		background: url('/images/squiggle-underline.png') no-repeat center;
		background-size: 100% 100%;
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
		background: transparent;
		cursor: pointer;
		transition: background 0.2s, color 0.2s;
		text-decoration: none;
	}

	.btn-pill:hover { background: #000; color: #fff; }

	.hero-join {
		font-size: 28px;
		opacity: 0.6;
		margin-bottom: 24px;
	}

	.hero-arrow {
		opacity: 0.8;
	}

	/* ===== SUBHEADER ===== */
	.subheader {
		max-width: 1100px;
		margin: 0 auto;
		text-align: center;
		padding: 40px;
		font-size: 22px;
		line-height: 1.5;
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

	/* All sections use only border-bottom; the wrapper ::before provides the top line */
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
		min-height: 660px;
	}

	.juice-grid {
		grid-template-columns: 36% var(--b) 1fr;
	}

	.daydream-grid {
		grid-template-columns: 1fr var(--b) 36%;
	}

	.grid-divider {
		background: #000;
		position: relative;
	}

	/* Photo stack (two images stacked) */
	.photo-stack {
		display: flex;
		flex-direction: column;
	}

	.stack-photo {
		flex: 1;
		overflow: hidden;
	}

	.stack-photo img {
		width: 100%;
		height: 100%;
		object-fit: cover;
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
	}

	/* Two-column layout: text left, video right */
	.event-columns {
		display: flex;
		gap: 24px;
		position: relative;
		z-index: 2;
	}

	.daydream-columns {
		flex-direction: row-reverse;
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

	.video-thumb img {
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
	}

	.sticker.s1 { width: 120px; bottom: -30px; left: 20px; transform: rotate(12.5deg); }
	.sticker.s2 { width: 70px; bottom: -15px; left: 180px; transform: rotate(20.7deg); }
	.sticker.s3 { width: 110px; bottom: -35px; left: 280px; transform: rotate(-11.3deg); }
	.sticker.s4 { width: 70px; bottom: -20px; left: 420px; transform: rotate(-14.5deg); }

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

	/* Gradients */
	.juice-gradient {
		position: absolute;
		bottom: 0;
		right: 0;
		width: 64%;
		height: 55%;
		background: linear-gradient(to top, rgba(152,233,151,0.2), transparent);
		pointer-events: none;
	}

	.daydream-gradient {
		position: absolute;
		bottom: 0;
		left: 0;
		width: 64%;
		height: 55%;
		background: linear-gradient(to top, rgba(255,137,200,0.17), transparent);
		pointer-events: none;
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
		gap: 12px;
		white-space: nowrap;
		animation: marquee-scroll 60s linear infinite;
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
		min-height: 600px;
	}

	.col-divider-v { background: #000; }

	.three-col-cell {
		position: relative;
		overflow: hidden;
	}

	.col-inner {
		position: relative;
		z-index: 1;
		padding: 24px 20px;
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
	}

	.col-desc {
		font-size: 22px;
		line-height: 1.4;
	}

	/* ===== GAMES HEADING (inside bordered area) ===== */
	.games-heading-area {
		text-align: center;
		padding: 80px 40px 60px;
		border-top: var(--b) solid #000;
		margin-top: calc(-1 * var(--b));
	}

	.games-heading {
		font-family: 'Zarathustra', Georgia, serif;
		font-size: 60px;
		font-weight: 400;
		margin-bottom: 12px;
	}

	.games-sub {
		font-size: 24px;
		opacity: 0.6;
	}

	/* ===== GAMES SHOWCASE (inside bordered area) ===== */
	.games-showcase {
		position: relative;
		border-top: var(--b) solid #000;
		border-bottom: var(--b) solid #000;
		margin-top: calc(-1 * var(--b));
		overflow: visible;
	}

	.games-pattern-strip {
		position: absolute;
		left: 0;
		right: 0;
		height: 40px;
		background: url('/images/pattern.png') repeat;
		background-size: 40px 40px;
		opacity: 0.03;
		pointer-events: none;
	}

	.games-pattern-strip.top { top: 0; }
	.games-pattern-strip.bottom { bottom: 0; }

	.games-carousel {
		display: flex;
		align-items: stretch;
		justify-content: center;
		position: relative;
		z-index: 1;
	}

	.side-card {
		width: 120px;
		border: var(--b) solid #000;
		display: flex;
		flex-direction: column;
		align-items: center;
		flex-shrink: 0;
	}

	.blue-tint { background: linear-gradient(180deg, rgba(58,157,210,0.15), rgba(255,255,255,0.15)); }
	.purple-tint { background: linear-gradient(180deg, rgba(96,93,190,0.15), rgba(255,255,255,0.15)); }

	.side-thumb-wrap {
		width: 76px;
		height: 76px;
		border: var(--b) solid #000;
		overflow: hidden;
		margin-top: 48px;
		flex-shrink: 0;
	}

	.side-thumb-wrap img { width: 100%; height: 100%; object-fit: cover; }

	.side-hline {
		width: calc(100% - 10px);
		height: var(--b);
		background: #000;
		margin-top: auto;
	}

	.side-bars {
		display: flex;
		gap: 24px;
		padding: 30px 0;
	}

	.side-vbar {
		width: var(--b);
		height: 80px;
		background: #000;
	}

	.main-game-card {
		width: 560px;
		border: var(--b) solid #000;
		position: relative;
		overflow: visible;
		flex-shrink: 0;
	}

	.game-cover { border-bottom: var(--b) solid #000; }

	.game-cover img {
		width: 100%;
		height: 340px;
		object-fit: cover;
		display: block;
	}

	.game-meta-area {
		padding: 20px 24px;
		background: linear-gradient(to bottom, rgba(255,255,255,0.9), rgba(96,93,190,0.1));
		border-bottom: var(--b) solid #000;
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

	.meta-dot { font-size: 12px; }
	.faded { opacity: 0.5; }

	.game-description {
		font-size: 24px;
		line-height: 1.45;
	}

	.game-nav {
		display: flex;
		height: 82px;
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
	}

	.nav-cell:last-child { border-right: none; }

	.nav-arrow-cell { width: 118px; flex-shrink: 0; }
	.nav-play-cell { flex: 1; }

	.nav-cell img { width: 28px; height: 28px; object-fit: contain; }
	.play-icon { transform: rotate(90deg); }

	/* ===== DONATE BORDERED WRAPPER ===== */
	.donate-bordered-wrapper {
		position: relative;
		max-width: 1440px;
		margin: 0 auto;
	}

	/* Full-width top line via pseudo */
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
		padding: 80px 40px 60px;
		text-align: center;
	}

	.donate-heading {
		font-family: 'Zarathustra', Georgia, serif;
		font-size: 50px;
		font-weight: 400;
		line-height: 1.2;
	}

	.donate-columns {
		display: grid;
		grid-template-columns: 1fr var(--b) 1fr;
		border: var(--b) solid #000;
	}

	.donate-divider { background: #000; }

	.donate-col {
		position: relative;
		min-height: 700px;
	}

	.donate-col-pattern {
		position: absolute;
		inset: 0;
		background:
			linear-gradient(180deg, rgba(255,255,255,0) 0%, rgba(255,255,255,1) 73%),
			url('/images/pattern.png') repeat;
		background-size: auto, 40px 40px;
		opacity: 0.03;
		pointer-events: none;
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
		flex: 1;
	}

	.donate-col-body p { margin-bottom: 16px; }

	.donate-btn {
		margin: 24px auto 0;
		background: #fff;
	}

	/* ===== LOGO STRIP ===== */
	.logo-strip {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		margin: 0 162px;
		height: 170px;
		border: var(--b) solid #000;
		border-top: none;
		position: relative;
		z-index: 2;
	}

	.logo-cell {
		border-right: var(--b) solid #000;
	}

	.logo-cell:last-child { border-right: none; }

	/* ===== FOOTER ===== */
	.footer {
		background: #000;
		color: #fff;
		overflow: hidden;
	}

	.footer-black-line { height: 4px; background: #000; }
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
	.footer-dot { opacity: 0.5; }

	.footer-tile {
		height: 250px;
		background: url('https://cdn.hackclub.com/019ccfbc-3b4c-7b04-a32a-8d3d940174c4/footer-tile.png') repeat-x;
		background-size: auto 140%;
		background-position: center calc(100% + 30px);
	}

	/* ===== RESPONSIVE ===== */
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

		.hero { height: auto; min-height: 600px; padding: 100px 20px; max-height: none; }
		.hero-heading-top { font-size: 36px; }
		.hero-heading-big { font-size: 64px; }
		.hero-join { font-size: 22px; }
		.game-shot { width: 240px; height: 180px; }

		.juice-grid, .daydream-grid { grid-template-columns: 1fr; }
		.grid-divider { height: var(--b); }
		.photo-stack { max-height: 400px; }

		.event-columns { flex-direction: column; }
		.daydream-columns { flex-direction: column; }
		.event-title { font-size: 42px; }
		.event-desc { font-size: 18px; }
		.video-thumb img { width: 280px; height: 160px; }
		.marquee-section { height: auto; }
		.marquee-clip { padding: 20px 0; }

		.three-col-grid { grid-template-columns: 1fr; }
		.col-divider-v { height: var(--b); width: 100%; }
		.col-title { font-size: 36px; }
		.col-desc { font-size: 18px; }

		.side-card { display: none; }
		.main-game-card { width: 100%; max-width: 600px; }
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

		.logo-strip { height: 120px; grid-template-columns: repeat(4, 1fr); }

		.footer-top { padding: 48px 40px 32px; }
		.footer-tagline { font-size: 22px; }
		.footer-links a { font-size: 22px; }
	}

	@media (max-width: 768px) {
		.bordered-content { margin: 0 16px; }
		.donate-section { margin: 0 16px; }
		.logo-strip { margin: 0 16px; }
		.side-pattern { display: none; }
		.border-line { display: none; }
		.line-dot.dot-top-left, .line-dot.dot-top-right, .line-dot.dot-bottom-left, .line-dot.dot-bottom-right { display: none; }
		.marquee-line-left, .marquee-line-right { display: none; }

		.hero-heading-top { font-size: 26px; }
		.hero-heading-big { font-size: 44px; }
		.hero-join { font-size: 18px; }
		.btn-pill { width: 180px; height: 60px; font-size: 18px; }
		.game-shot { width: 160px; height: 120px; }

		.event-columns { flex-direction: column; }
		.daydream-columns { flex-direction: column; }
		.video-thumb img { width: 100%; height: auto; }
		.sticker-cluster { display: none; }

		.event-photo-row { flex-wrap: wrap; }
		.row-photo { min-width: 50%; }
		.row-photo img { height: 120px; }

		.col-title { font-size: 28px; }
		.col-desc { font-size: 16px; }
		.col-thumb img { width: 100%; }

		.games-heading { font-size: 32px; }
		.games-sub { font-size: 16px; }
		.game-nav { height: 70px; }
		.nav-arrow-cell { width: 80px; }

		.donate-heading { font-size: 32px; }
		.donate-col-inner { padding: 32px 24px; }
		.donate-col-title { font-size: 26px; }
		.donate-col-body { font-size: 16px; }

		.footer-top { padding: 32px 20px 24px; }
		.footer-tagline { font-size: 18px; }
		.footer-links a { font-size: 16px; }
		.footer-tile { height: 150px; }

		.logo-strip { height: 80px; grid-template-columns: repeat(3, 1fr); }
	}
</style>
