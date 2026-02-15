<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import './style.css';
	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title>Akiss~~</title>
</svelte:head>

{@render children()}
