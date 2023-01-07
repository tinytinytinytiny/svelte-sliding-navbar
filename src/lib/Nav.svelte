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

<button
	aria-controls="main-menu"
	aria-expanded={$open}
	aria-label={$open ? 'Close menu' : 'Open menu'}
	class="nav-toggler"
	on:click={handleNavToggle}
>
	<svg
		aria-hidden="true"
		class="ham hamRotate ham1"
		viewBox="0 0 100 100"
		width="48"
		data-state={$open ? 'close' : 'burger'}
	>
		<path
			class="line top"
			d="m 30,33 h 40 c 0,0 9.044436,-0.654587 9.044436,-8.508902 0,-7.854315 -8.024349,-11.958003 -14.89975,-10.85914 -6.875401,1.098863 -13.637059,4.171617 -13.637059,16.368042 v 40"
		/>
		<path class="line middle" d="m 30,50 h 40" />
		<path
			class="line bottom"
			d="m 30,67 h 40 c 12.796276,0 15.357889,-11.717785 15.357889,-26.851538 0,-15.133752 -4.786586,-27.274118 -16.667516,-27.274118 -11.88093,0 -18.499247,6.994427 -18.435284,17.125656 l 0.252538,40"
		/>
	</svg>
</button>
<nav id="main-menu" aria-label="Main menu" data-state={$open ? 'nav-expanded' : 'nav-collapsed'}>
	<div class="nav-inner">
		<div class="nav-body">
			<div class="nav-logo">
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
</nav>

<style>
	nav {
		height: 100%;
		max-width: 100%;
		width: var(--nav-width);
	}

	.nav-inner {
		height: 100%;
		width: 100%;
	}

	.nav-body {
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

	.nav-logo {
		background-color: var(--bg);
	}

	.nav-logo img {
		mix-blend-mode: multiply;
	}

	nav h2 {
		margin-block-start: var(--space-xs);
	}

	nav ul {
		list-style: none;
		padding: 0;
	}

	nav ul::before,
	nav footer::before {
		content: '';
		background-color: rgba(0, 0, 0, 0.16);
		display: block;
		height: 1px;
		margin-block: var(--stack-space);
		width: 100%;
	}

	nav a {
		color: inherit;
		display: block;
		padding-block: calc(var(--space-s) / 2);
		position: relative;
		text-decoration: none;
	}

	nav a::before {
		content: '';
		inset: 0 calc(-1 * var(--padding));
		position: absolute;
	}

	nav a:hover::before {
		background-color: rgba(0, 0, 0, 0.08);
	}

	.hamRotate[data-state='close'] {
		transform: rotate(45deg);
	}

	.line {
		fill: none;
		transition: stroke-dasharray 400ms, stroke-dashoffset 400ms;
		stroke: currentColor;
		stroke-width: 5.5;
		stroke-linecap: round;
	}

	.ham1 .top {
		stroke-dasharray: 40 139;
	}

	.ham1 .bottom {
		stroke-dasharray: 40 180;
	}

	.ham1[data-state='close'] .top {
		stroke-dashoffset: -98px;
	}

	.ham1[data-state='close'] .bottom {
		stroke-dashoffset: -138px;
	}

	@media (max-width: 50rem) {
		nav {
			position: fixed;
			top: 0;
			transform: translateX(calc(-1 * var(--nav-width)));
			z-index: 10;
		}

		nav[data-state='nav-expanded'] {
			transform: none;
		}

		.nav-inner {
			background-color: var(--bg);
		}

		.nav-body {
			padding-block-start: calc(var(--padding) + var(--nav-button-size) + var(--stack-space));
		}

		nav::before {
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

		nav[data-state='nav-expanded']::before {
			opacity: 1;
		}

		.nav-toggler {
			display: block;
		}
	}
</style>
