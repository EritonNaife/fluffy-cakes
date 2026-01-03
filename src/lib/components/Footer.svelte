<script lang="ts">
	interface QuickLink {
		href: string;
		label: string;
	}

	const quickLinks: QuickLink[] = [
		{ href: '/menu', label: 'Menu & Pricing' },
		{ href: '/gallery', label: 'Gallery' },
		{ href: '/about', label: 'About Us' },
		{ href: '/order', label: 'Place Order' }
	];

	const currentYear = new Date().getFullYear();
</script>

<footer class="border-t border-border bg-secondary/50">
	<div class="container mx-auto max-w-300 py-16">
		<div class="grid gap-12 md:grid-cols-2 lg:grid-cols-4">
			<!-- Brand -->
			<div class="lg:col-span-2">
				<h3 class="mb-4 font-display text-2xl font-bold text-chocolate">Fluffy Cakes</h3>
				<p class="mb-6 max-w-md text-muted-foreground">
					Handcrafted with love, baked to perfection. Every cake tells a story, and we'd love to be
					part of yours.
				</p>
				<div class="flex gap-4">
					<a
						href="https://instagram.com"
						target="_blank"
						rel="noopener noreferrer"
						class="flex h-10 w-10 items-center justify-center rounded-full bg-primary/10 text-primary transition-colors hover:bg-primary hover:text-primary-foreground"
						aria-label="Instagram"
					>
						<svg
							class="h-5 w-5"
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
							<rect width="20" height="20" x="2" y="2" rx="5" ry="5" />
							<path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z" />
							<line x1="17.5" x2="17.51" y1="6.5" y2="6.5" />
						</svg>
					</a>
					<a
						href="https://wa.me/1234567890"
						target="_blank"
						rel="noopener noreferrer"
						class="flex h-10 w-10 items-center justify-center rounded-full bg-primary/10 text-primary transition-colors hover:bg-primary hover:text-primary-foreground"
						aria-label="WhatsApp"
					>
						<svg
							class="h-5 w-5"
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
							<path d="M3 21l1.65-3.8a9 9 0 1 1 3.4 2.9z" />
							<path d="M9 10a.5.5 0 0 0 1 0V9a.5.5 0 0 0-1 0v1a0 0 0 0 0 0 0" />
						</svg>
					</a>
					<a
						href="mailto:hello@fluffycakes.com"
						class="flex h-10 w-10 items-center justify-center rounded-full bg-primary/10 text-primary transition-colors hover:bg-primary hover:text-primary-foreground"
						aria-label="Email"
					>
						<svg
							class="h-5 w-5"
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
							<rect width="20" height="16" x="2" y="4" rx="2" />
							<path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7" />
						</svg>
					</a>
				</div>
			</div>

			<!-- Quick Links -->
			<div>
				<h4 class="mb-4 font-display font-semibold text-foreground">Quick Links</h4>
				<ul class="space-y-3">
					{#each quickLinks as link (link.href)}
						<li>
							<a
								href={link.href}
								class="text-muted-foreground transition-colors hover:text-chocolate"
							>
								{link.label}
							</a>
						</li>
					{/each}
				</ul>
			</div>

			<!-- Contact -->
			<div>
				<h4 class="mb-4 font-display font-semibold text-foreground">Visit Us</h4>
				<div class="space-y-3 text-muted-foreground">
					<div class="flex items-start gap-2">
						<svg
							class="mt-0.5 h-5 w-5 text-caramel"
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
							<path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z" />
							<circle cx="12" cy="10" r="3" />
						</svg>
						<span>
							Rua Formosa 339<br />
							4000-252 Porto
						</span>
					</div>
					<p class="text-sm">
						<span class="font-medium text-foreground">Pickup Hours:</span><br />
						Tue - Sat: 10am - 6pm<br />
						Sun: 11am - 4pm
					</p>
				</div>
			</div>
		</div>

		<div class="mt-12 border-t border-border pt-8 text-center text-sm text-muted-foreground">
			<p>&copy; {currentYear} Fluffy Cakes. Made with 🤎</p>
		</div>
	</div>
</footer>

<style>
	/* Add any component-specific styles here if needed */
</style>
