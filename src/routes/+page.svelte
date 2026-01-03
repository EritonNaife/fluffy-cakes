<script lang="ts">
	import { fade, fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import { inview } from 'svelte-inview';
	import { ArrowRight, Sparkles, Calendar, MessageCircle } from '@lucide/svelte';
	import { Button } from '$lib/components/ui/button';
	import cupcakesImg from '$lib/assets/cupcakes.jpg';
	import weddingCakeImg from '$lib/assets/wedding-cake.jpg';

	interface Testimonial {
		name: string;
		event: string;
		content: string;
		rating: number;
	}

	const categories = [
		{
			title: 'Custom Cakes',
			description: "Birthday, anniversary, or just because - we'll create your dream cake.",
			image: weddingCakeImg,
			link: '/order',
			cta: 'Start Your Order'
		},
		{
			title: 'Ready to Eat',
			description: 'Cake slices, cake in a pot, and treats available for next-day pickup.',
			image: cupcakesImg,
			link: '/menu',
			cta: 'View Menu'
		}
	];

	const testimonials: Testimonial[] = [
		{
			name: 'Sarah M.',
			event: 'Wedding Cake',
			content:
				"Fluffy Cakes made our wedding day even more special. The cake was not only stunning but absolutely delicious. Every guest asked for the bakery's name!",
			rating: 5
		},
		{
			name: 'Michael T.',
			event: 'Birthday Order',
			content:
				"Ordered a custom cake for my daughter's 5th birthday. The unicorn design was beyond our expectations. She was over the moon!",
			rating: 5
		},
		{
			name: 'Lisa K.',
			event: 'Regular Customer',
			content:
				'The cupcakes are my go-to for every office celebration. Fresh, flavorful, and everyone fights over the salted caramel ones!',
			rating: 5
		}
	];

	let headerVisible = $state(false);
	let cardsVisible = $state<boolean[]>(testimonials.map(() => false));

	function handleHeaderInView(event: CustomEvent<ObserverEventDetails>) {
		if (event.detail.inView && !headerVisible) {
			headerVisible = true;
		}
	}

	function handleCardInView(index: number) {
		return (event: CustomEvent<ObserverEventDetails>) => {
			if (event.detail.inView && !cardsVisible[index]) {
				cardsVisible[index] = true;
			}
		};
	}

	// Svelte 5 uses $props() for any incoming props
	// let { propName } = $props();
</script>

<section class="relative flex min-h-screen items-center justify-center overflow-hidden">
	<div class="absolute inset-0">
		<img
			src=""
			alt="Beautiful artisanal chocolate cake with caramel drip"
			class="h-full w-full object-cover"
		/>
		<div
			class="absolute inset-0 bg-linear-to-b from-background/60 via-background/40 to-background"
		></div>
	</div>

	<div class="relative z-10 container pt-24 pb-16">
		<div class="mx-auto max-w-3xl p-8 text-center">
			<div in:fly={{ y: 30, duration: 600 }}>
				<span
					class="mb-6 inline-flex items-center gap-2 rounded-full bg-blush/80 px-4 py-2 text-sm font-medium text-chocolate backdrop-blur-sm"
				>
					<Sparkles class="h-4 w-4" />
					Home Bakery
				</span>
			</div>

			<h1
				in:fly={{ y: 30, duration: 600, delay: 100 }}
				class="mb-6 font-display text-5xl leading-tight font-bold text-chocolate md:text-7xl"
			>
				Handcrafted with Love,
				<br />
				<span class="text-caramel">Baked to Perfection</span>
			</h1>

			<p
				in:fly={{ y: 30, duration: 600, delay: 200 }}
				class="mx-auto mb-10 max-w-2xl text-lg text-chocolate-light md:text-xl"
			>
				From custom celebration cakes to our irresistible ready-to-eat treats, every creation is
				made fresh with premium ingredients and endless love.
			</p>

			<div
				in:fly={{ y: 30, duration: 600, delay: 300 }}
				class="flex flex-col justify-center gap-4 sm:flex-row"
			>
				<Button href="/order" variant="hero" size="xl" class="group w-full sm:w-auto">
					<Calendar class="h-5 w-5" />
					Order Custom Cake
					<ArrowRight class="h-5 w-5 transition-transform group-hover:translate-x-1" />
				</Button>

				<Button href="/menu" variant="hero-outline" size="xl" class="w-full sm:w-auto">
					Shop Ready-to-Eat
				</Button>
			</div>
		</div>
	</div>

	<div in:fade={{ delay: 1000 }} class="absolute bottom-1 left-1/2 -translate-x-1/2 md:bottom-8">
		<div class="flex flex-col items-center gap-2 text-chocolate-light">
			<span class="text-xs tracking-wider uppercase">Scroll to explore</span>
			<div
				class="animate-bounce-slow flex h-10 w-6 justify-center rounded-full border-2 border-chocolate-light/50 pt-2"
			>
				<div class="h-1.5 w-1.5 rounded-full bg-chocolate-light/50"></div>
			</div>
		</div>
	</div>
</section>

<section class="bg-secondary/30 py-24">
	<div class="container mx-auto max-w-300 p-8">
		<div in:fly={{ y: 20, duration: 500 }} class="mb-16 text-center">
			<h2 class="mb-4 font-display text-4xl font-bold text-chocolate md:text-5xl">
				What Are You Craving?
			</h2>
			<p class="mx-auto max-w-2xl text-lg text-muted-foreground">
				Whether you're planning ahead or need something sweet today, we've got you covered.
			</p>
		</div>

		<div class="grid gap-8 md:grid-cols-2">
			{#each categories as category, index}
				<div in:fly={{ y: 30, duration: 500, delay: index * 100 }}>
					<a
						href={category.link}
						class="group relative block overflow-hidden rounded-2xl bg-card shadow-soft transition-all duration-500 hover:shadow-elevated"
					>
						<div class="aspect-4/3 overflow-hidden">
							<img
								src={category.image}
								alt={category.title}
								class="h-full w-full object-cover transition-transform duration-700 group-hover:scale-105"
							/>
						</div>

						<div
							class="absolute inset-0 bg-linear-to-t from-espresso/80 via-espresso/20 to-transparent"
						></div>

						<div class="absolute right-0 bottom-0 left-0 p-8">
							<h3 class="mb-2 font-display text-3xl font-bold text-cream">
								{category.title}
							</h3>
							<p class="mb-4 text-cream/80">{category.description}</p>
							<span
								class="inline-flex items-center gap-2 font-medium text-caramel transition-all group-hover:gap-3"
							>
								{category.cta}
								<ArrowRight class="h-5 w-5" />
							</span>
						</div>
					</a>
				</div>
			{/each}
		</div>
	</div>
</section>

<section class="py-24">
	<div class="container mx-auto max-w-300 p-8">
		<div use:inview on:inview_change={handleHeaderInView} class="mb-16 text-center">
			{#if headerVisible}
				<div in:fly={{ y: 20, duration: 500, easing: quintOut }}>
					<h2 class="mb-4 font-display text-4xl font-bold text-chocolate md:text-5xl">
						Sweet Words from Our Customers
					</h2>
					<p class="mx-auto max-w-2xl text-lg text-muted-foreground">
						Nothing makes us happier than seeing our cakes bring joy to your celebrations.
					</p>
				</div>
			{/if}
		</div>

		<div class="grid gap-8 md:grid-cols-3">
			{#each testimonials as testimonial, index (testimonial.name)}
				<div use:inview on:inview_change={handleCardInView(index)}>
					{#if cardsVisible[index]}
						<div
							in:fly={{ y: 30, duration: 500, delay: index * 100, easing: quintOut }}
							class="relative rounded-2xl bg-card p-8 shadow-soft transition-shadow hover:shadow-elevated"
						>
							<svg
								class="absolute top-6 right-6 h-10 w-10 text-blush"
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
								<path
									d="M3 21c3 0 7-1 7-8V5c0-1.25-.756-2.017-2-2H4c-1.25 0-2 .75-2 1.972V11c0 1.25.75 2 2 2 1 0 1 0 1 1v1c0 1-1 2-2 2s-1 .008-1 1.031V20c0 1 0 1 1 1z"
								/>
								<path
									d="M15 21c3 0 7-1 7-8V5c0-1.25-.757-2.017-2-2h-4c-1.25 0-2 .75-2 1.972V11c0 1.25.75 2 2 2h.75c0 2.25.25 4-2.75 4v3c0 1 0 1 1 1z"
								/>
							</svg>

							<div class="mb-4 flex gap-1">
								{#each Array(testimonial.rating) as _, i}
									<svg
										class="h-5 w-5 fill-caramel text-caramel"
										xmlns="http://www.w3.org/2000/svg"
										width="24"
										height="24"
										viewBox="0 0 24 24"
										fill="currentColor"
										stroke="currentColor"
										stroke-width="2"
										stroke-linecap="round"
										stroke-linejoin="round"
									>
										<polygon
											points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"
										/>
									</svg>
								{/each}
							</div>

							<p class="mb-6 leading-relaxed text-foreground">
								"{testimonial.content}"
							</p>

							<div class="border-t border-border pt-4">
								<p class="font-display font-semibold text-chocolate">
									{testimonial.name}
								</p>
								<p class="text-sm text-muted-foreground">{testimonial.event}</p>
							</div>
						</div>
					{/if}
				</div>
			{/each}
		</div>
	</div>
</section>

<section class="relative overflow-hidden bg-primary py-24">
	<div class="containre mx-auto max-w-[1200px] p-8">
		<div class="absolute inset-0 opacity-10">
			<div class="absolute top-0 left-1/4 h-96 w-96 rounded-full bg-caramel blur-3xl"></div>
			<div class="absolute right-1/4 bottom-0 h-64 w-64 rounded-full bg-blush blur-3xl"></div>
		</div>

		<div class="relative z-10 container">
			<div in:fly={{ y: 20, duration: 500 }} class="mx-auto max-w-3xl text-center">
				<h2 class="mb-6 font-display text-4xl font-bold text-primary-foreground md:text-5xl">
					Ready to Make Your Celebration Special?
				</h2>
				<p class="mx-auto mb-10 max-w-2xl text-lg text-primary-foreground/80">
					Let's create something beautiful together. Whether it's a custom masterpiece or a dozen of
					our famous cupcakes, we're here to sweeten your moments.
				</p>

				<div class="flex flex-col justify-center gap-4 sm:flex-row">
					<Button href="/order" variant="secondary" size="xl" class="group w-full sm:w-auto">
						Start Your Order
						<ArrowRight class="h-5 w-5 transition-transform group-hover:translate-x-1" />
					</Button>

					<Button
						href="https://wa.me/1234567890"
						target="_blank"
						rel="noopener noreferrer"
						variant="outline"
						size="xl"
						class="w-full border-primary-foreground/30 text-primary-foreground hover:bg-primary-foreground hover:text-primary sm:w-auto"
					>
						<MessageCircle class="h-5 w-5" />
						Chat on WhatsApp
					</Button>
				</div>
			</div>
		</div>
	</div>
</section>

<style>
	/* Standard Tailwind doesn't have a 1.5s loop for y-axis movement, 
       so we can add a quick custom animation or use a utility */
	@keyframes bounce-slow {
		0%,
		100% {
			transform: translateY(0);
		}
		50% {
			transform: translateY(8px);
		}
	}
	.animate-bounce-slow {
		animation: bounce-slow 1.5s infinite;
	}
</style>
