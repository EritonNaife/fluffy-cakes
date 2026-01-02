<script lang="ts">
	import { page } from '$app/stores';
	import { slide, fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';

	interface NavLink {
		href: string;
		label: string;
	}

	const navLinks: NavLink[] = [
		{ href: '/', label: 'Home' },
		{ href: '/menu', label: 'Menu & Pricing' },
		{ href: '/gallery', label: 'Gallery' },
		{ href: '/about', label: 'About' },
		{ href: '/order', label: 'Order' }
	];

	let isOpen = $state(false);

	// Get current pathname from the page store
	$effect(() => {
		// Close mobile menu when route changes
		isOpen = false;
	});
</script>

<header class="fixed top-0 right-0 left-0 z-50">
	<nav class="glass mx-4 mt-4 rounded-2xl px-6 py-4 lg:mx-auto lg:max-w-6xl">
		<div class="flex items-center justify-between">
			<!-- Logo -->
			<a href="/" class="flex items-center gap-2">
				<span class="font-display text-2xl font-bold text-chocolate"> Fluffy Cakes </span>
			</a>

			<!-- Desktop Navigation -->
			<div class="hidden items-center gap-1 lg:flex">
				{#each navLinks as link (link.href)}
					<a
						href={link.href}
						class="relative rounded-lg px-4 py-2 text-sm font-medium transition-colors duration-200 {$page
							.url.pathname === link.href
							? 'text-chocolate'
							: 'text-muted-foreground hover:text-foreground'}"
					>
						{link.label}
						{#if $page.url.pathname === link.href}
							<div
								class="absolute inset-0 -z-10 rounded-lg bg-secondary"
								style="view-transition-name: activeNav"
								transition:fly={{ duration: 300, easing: quintOut }}
							/>
							<div></div>
						{/if}
					</a>
				{/each}
			</div>

			<!-- Mobile Menu Button -->
			<button onclick={() => (isOpen = !isOpen)} class="p-2 lg:hidden" aria-label="Toggle menu">
				{#if isOpen}
					<svg
						class="h-6 w-6 text-chocolate"
						xmlns="http://www.w3.org/2000/svg"
						width="24"
						height="24"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
					>
						<path d="M18 6 6 18" /><path d="m6 6 12 12" />
					</svg>
				{:else}
					<svg
						class="h-6 w-6 text-chocolate"
						xmlns="http://www.w3.org/2000/svg"
						width="24"
						height="24"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="2"
						stroke-linecap="round"
						stroke-linejoin="round"
					>
						<line x1="4" x2="20" y1="12" y2="12" /><line x1="4" x2="20" y1="6" y2="6" /><line
							x1="4"
							x2="20"
							y1="18"
							y2="18"
						/>
					</svg>
				{/if}
			</button>
		</div>

		<!-- Mobile Navigation -->
		{#if isOpen}
			<div transition:slide={{ duration: 200, easing: quintOut }} class="overflow-hidden lg:hidden">
				<div class="flex flex-col gap-2 pt-4 pb-2">
					{#each navLinks as link, index (link.href)}
						<div in:fly={{ x: -20, duration: 200, delay: index * 50, easing: quintOut }}>
							<a
								href={link.href}
								onclick={() => (isOpen = false)}
								class="block rounded-lg px-4 py-3 text-base font-medium transition-colors {$page.url
									.pathname === link.href
									? 'bg-secondary text-chocolate'
									: 'text-muted-foreground hover:bg-secondary/50 hover:text-foreground'}"
							>
								{link.label}
							</a>
						</div>
					{/each}
				</div>
			</div>
		{/if}
	</nav>
</header>

<style>
	/* Add any component-specific styles here if needed */
</style>
