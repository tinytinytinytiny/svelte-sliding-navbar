# svelte-sliding-navbar
<https://profound-custard-a03579.netlify.app/>  
responsive side sheet menu that pushes the website content to the side as it opens

![demo](demo.gif)

## Initialization
add `initial-scale=1` to meta viewport tag to prevent dpi-related bugs with css transform animation:

	<meta name="viewport" content="width=device-width,initial-scale=1" />

prevent horizontal overflow:

	html, body {
		overflow-x: hidden;
		overflow-x: -moz-hidden-unscrollable;
		overflow-x: clip;
	}

use `text-size-adjust` property to prevent font size from scaling in landscape orientation:

	html {
		-webkit-text-size-adjust: none;
		text-size-adjust: none;
	}

reset all elements to border-box and add transitions:

	*, *::before, *::after {
		box-sizing: border-box;
		transition: transform 0.3s ease;
	}

## Layout
	<body data-sveltekit-preload-data="hover">
		<div class="layout">
			<nav aria-label="Main menu">
				<button
					aria-controls="main-menu"
					aria-expanded="false"
					aria-label="Open menu"
					class="nav-toggler"
					type="button"
				>
				</button>
				<div id="main-menu" class="nav-menu"></div>
			</nav>
			<main></main>
		</div>
	</body>

the `<nav>` can be abstracted into a separate component:

	<body data-sveltekit-preload-data="hover">
		<div class="layout">
			<Nav />
			<main></main>
		</div>
	</body>

the `.layout` class will be a 3-column grid to create a sidebar layout with the body content centered in the viewport:

	.layout {
		--max-content-width: 50rem;
		--nav-width: 18rem;
		display: grid;
		grid-template-columns: 1fr minmax(auto, var(--max-content-width)) 1fr;
	}

	nav {
		display: contents;
	}

	.nav-menu {
		height: 100%;
		width: var(--nav-width);
	}

	.nav-toggler {
		display: none;
		position: fixed;
		top: 0;
		z-index: 20;
	}

at the breakpoint of **50rem** viewport width, the layout stops being a grid and the body content fills the entire viewport. the navigation menu is pushed to the left:

	@media (max-width: 50rem) {
		.layout {
			display: contents;
		}

		.nav-menu {
			position: fixed;
			top: 0;
			transform: translateX(calc(-1 * var(--nav-width)));
			z-index: 10;
		}

		.nav-toggler {
			display: block;
		}
	}

## Interactivity
use store to share nav component’s open state with the entire page:

Nav.svelte

	<script context="module">
		import { writable } from 'svelte/store';

		export const open = writable(false);
	</script>

	<script>
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
		<div id="main-menu" class="nav-menu"></div>
	</nav>

+page.svelte

	<script>
		import Nav, { open } from '$lib/Nav.svelte';
	</script>

	<Nav />
	<main data-state={$open ? 'nav-expanded' : 'nav-collapsed'}></main>

then, adjust css transforms for menu open state:

	@media (max-width: 50rem) {
		[aria-expanded="true"] + .nav-menu {
			transform: none;
		}

		main[data-state="nav-expanded"] {
			transform: translateX(var(--nav-width));
		}
	}
