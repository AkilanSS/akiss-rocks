<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import './style.css';
	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<link rel="stylesheet" href="style.css">
	<title>Akiss~~</title>
</svelte:head>

{@render children()}
