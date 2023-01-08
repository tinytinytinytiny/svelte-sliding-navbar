<script context="module">
	import { writable } from 'svelte/store';

	export const open = writable(false);
</script>

<script>
	import links from '$lib/data/links.json';

	function handleNavToggle() {
		$open = !$open;
	}
</script>

<nav aria-label="Main menu">
	<button
		aria-controls="main-menu"
		aria-expanded={$open}
		aria-label={$open ? 'Close menu' : 'Open menu'}
		class="nav-toggler"
		type="button"
		on:click={handleNavToggle}
	>
		<svg aria-hidden="true" class="hamburger" viewBox="0 0 100 100" width="48">
			<path
				class="hamburger__line-top"
				d="m 30,33 h 40 c 0,0 9.044436,-0.654587 9.044436,-8.508902 0,-7.854315 -8.024349,-11.958003 -14.89975,-10.85914 -6.875401,1.098863 -13.637059,4.171617 -13.637059,16.368042 v 40"
			/>
			<path d="m 30,50 h 40" />
			<path
				class="hamburger__line-bottom"
				d="m 30,67 h 40 c 12.796276,0 15.357889,-11.717785 15.357889,-26.851538 0,-15.133752 -4.786586,-27.274118 -16.667516,-27.274118 -11.88093,0 -18.499247,6.994427 -18.435284,17.125656 l 0.252538,40"
			/>
		</svg>
	</button>
	<div class="nav-menu" id="main-menu">
		<div class="nav-menu__inner">
			<div class="nav-menu__body">
				<div class="logo">
					<img src="/favicon.png" width="128" height="128" alt="" />
				</div>
				<h2>Sliding Navbar Demo</h2>
				<ul>
					{#each links as { title, url }}
						<li><a href={url}>{title}</a></li>
					{/each}
				</ul>
				<footer>Copyright (c) 2023 Copyright Holder All Rights Reserved.</footer>
			</div>
		</div>
	</div>
</nav>

<style>
	nav {
		display: contents;
	}

	.nav-menu {
		height: 100%;
		max-width: 100%;
		width: var(--nav-width);
	}

	.nav-menu__inner {
		height: 100%;
		width: 100%;
	}

	.nav-menu__body {
		max-height: 100vh;
		max-height: 100dvh;
		padding: var(--padding);
		padding-bottom: calc(var(--padding) + env(safe-area-inset-bottom));
		position: sticky;
		overflow-y: auto;
		overscroll-behavior: contain;
		top: 0;
	}

	.nav-toggler {
		box-sizing: content-box;
		display: none;
		height: var(--nav-button-size);
		margin-inline-start: -12px;
		padding: var(--padding);
		position: fixed;
		top: 0;
		width: var(--nav-button-size);
		z-index: 20;
	}

	.logo {
		background-color: var(--bg);
	}

	.logo img {
		mix-blend-mode: multiply;
	}

	h2 {
		margin-block-start: var(--space-xs);
	}

	ul {
		list-style: none;
		padding: 0;
	}

	ul::before,
	footer::before {
		content: '';
		background-color: rgba(0, 0, 0, 0.16);
		display: block;
		height: 1px;
		margin-block: var(--stack-space);
		width: 100%;
	}

	a {
		color: inherit;
		display: block;
		padding-block: calc(var(--space-s) / 2);
		position: relative;
		text-decoration: none;
	}

	a::before {
		content: '';
		inset: 0 calc(-1 * var(--padding));
		position: absolute;
	}

	a:hover::before {
		background-color: rgba(0, 0, 0, 0.08);
	}

	[aria-expanded='true'] .hamburger {
		transform: rotate(45deg);
	}

	.hamburger > path {
		fill: none;
		transition: stroke-dasharray 400ms, stroke-dashoffset 400ms;
		stroke: currentColor;
		stroke-width: 5.5;
		stroke-linecap: round;
	}

	.hamburger__line-top {
		stroke-dasharray: 40 139;
	}

	.hamburger__line-bottom {
		stroke-dasharray: 40 180;
	}

	[aria-expanded='true'] .hamburger__line-top {
		stroke-dashoffset: -98px;
	}

	[aria-expanded='true'] .hamburger__line-bottom {
		stroke-dashoffset: -138px;
	}

	@media (max-width: 50rem) {
		.nav-menu {
			position: fixed;
			top: 0;
			transform: translateX(calc(-1 * var(--nav-width)));
			z-index: 10;
		}

		[aria-expanded='true'] + .nav-menu {
			transform: none;
		}

		.nav-menu__inner {
			background-color: var(--bg);
		}

		.nav-menu__body {
			padding-block-start: calc(var(--padding) + var(--nav-button-size) + var(--stack-space));
		}

		.nav-menu::before {
			background-color: rgba(0, 0, 0, 0.05);
			background-image: linear-gradient(
				90deg,
				rgba(0, 0, 0, 0.7) calc(var(--nav-width) / 2),
				rgba(0, 0, 0, 0.25) calc(var(--nav-width) * 2)
			);
			content: '';
			height: 100vh;
			height: 100lvh;
			opacity: 0;
			position: fixed;
			width: calc(100vw + var(--nav-width));
			width: calc(100lvw + var(--nav-width));
			z-index: -1;
		}

		[aria-expanded='true'] + .nav-menu::before {
			opacity: 1;
		}

		.nav-toggler {
			display: block;
		}
	}
</style>
