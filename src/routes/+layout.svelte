<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import { isLoggedIn } from '$lib/stores';
	import { page } from '$app/state';
    import { goto } from "$app/navigation";

	let { children } = $props();

	let showLogoutDialog = $state(false);
	function toggleLogoutDialog() {
		showLogoutDialog = !showLogoutDialog;
	}

	function handleLogout() {
		isLoggedIn.set(false);
		showLogoutDialog = false;
		goto("/");
	}
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{#if $isLoggedIn}
	<nav class="bg-blue-600 text-white p-4">
		<div class="container mx-auto flex justify-between items-center">
			<div>
				<a href="/" class="mr-4 {page.url.pathname === '/' ? 'font-bold' : ''}">Home</a>
				<a href="/about" class="mr-4 {page.url.pathname === '/about' ? 'font-bold' : ''}">About</a>
				<a href="/blog" class="{page.url.pathname === '/blog' ? 'font-bold' : ''}">Blog</a>
			</div>
			<button onclick={toggleLogoutDialog} class="text-white hover:text-gray-200" aria-label="Logout">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
				</svg>
			</button>
		</div>
	</nav>
{/if}

{#if showLogoutDialog}
	<div
		class="fixed inset-0 bg-black/50 flex items-center justify-center z-50"
		onclick={(e) => {
			// Only close if background (overlay) is clicked
			if (e.target === e.currentTarget) toggleLogoutDialog();
		}}
		onkeydown={(e) => {
			if (e.key === "Escape") toggleLogoutDialog();
		}}
		role="dialog"
		aria-modal="true"
		aria-labelledby="logout-title"
		tabindex="-1"
	>
		<div class="bg-white p-10 rounded-3xl shadow-2xl w-full max-w-md mx-4 relative">
			<button
				type="button"
				class="absolute top-4 right-4 text-gray-400 hover:text-gray-600 text-2xl"
				onclick={toggleLogoutDialog}
				aria-label="Close logout dialog"
			>
				&times;
			</button>

			<h2
				id="logout-title"
				class="text-center text-2xl font-bold mb-8 text-gray-800"
			>
				Confirm Logout
			</h2>

			<p class="text-center text-gray-600 mb-8">
				Are you sure you want to logout?
			</p>

			<div class="flex justify-center space-x-4">
				<button
					class="bg-gray-300 text-gray-800 px-6 py-2 rounded-lg hover:bg-gray-400 transition-colors"
					onclick={toggleLogoutDialog}
				>
					Cancel
				</button>
				<button
					class="bg-red-500 text-white px-6 py-2 rounded-lg hover:bg-red-600 transition-colors"
					onclick={handleLogout}
				>
					Logout
				</button>
			</div>
		</div>
	</div>
{/if}


{@render children()}
