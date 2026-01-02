<script lang="ts">
	import './layout.css';
	import Navbar from '$lib/components/Navbar.svelte';
	import Footer from '$lib/components/Footer.svelte';
</script>

<svelte:head>
	<title>Fluffy Cakes</title>
</svelte:head>

<main class="min-h-screen">
	<Navbar />
	<div class="min-h-screen"><slot /></div>

	<Footer />
</main>
