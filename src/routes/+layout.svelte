<script>
	import '$lib/styles/styles.scss';
</script>

<svelte:head>
	<title>Some of my frequently used web tools</title>
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
	<link
		href="https://fonts.googleapis.com/css2?family=Fugaz+One&family=Rubik:wght@400;700&display=swap"
		rel="stylesheet"
	/>
	<script
		defer
		data-domain="tools.craigwfox.com"
		src="https://plausible.io/js/plausible.js"></script>
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
		Built using SvelteKit
	</p>
</footer>
