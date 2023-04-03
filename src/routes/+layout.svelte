<script>
	import '$lib/styles/styles.scss';
</script>

<svelte:head>
	<title>BearBones Tools - Craig Fox</title>
	<meta name="description" content="Tools for converting pixels to rems and CSS color values." />
	<meta property="og:title" content="Home" />
	<meta property="og:type" content="website" />
	<meta
		property="og:description"
		content="Tools for converting pixels to rems and CSS color values."
	/>
	<meta property="og:url" content="https://tools.craigwfox.com/" />
	<meta name="theme-color" content="#172135" />
	<link rel="canonical" href="https://tools.craigwfox.com/" /><link
		rel="icon"
		href="/favicon.svg"
	/>
	<link rel="mask-icon" href="/favicon.svg" color="#172135" />
	<link rel="apple-touch-icon" href="/apple-touch-icon.png" />
	<link rel="manifest" href="/manifest.json" />

	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Fugaz+One&family=Rubik:wght@400;700&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<header class="site-header">
	<h1>🔨 BearBones tooling</h1>
</header>

<main id="maincontent">
	<div class="wrapper">
		<slot />
	</div>
</main>

<footer class="site-footer">
	<p>
		&copy; {new Date().getFullYear()}
		<a href="https://craigwfox.com">Craig Fox</a>
		<img src="/images/fox-icon.svg" alt="Illustration of fox head" />
		// Built using SvelteKit
	</p>
</footer>
