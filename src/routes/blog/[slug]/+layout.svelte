<script lang="ts">
	import { goto } from '$app/navigation';

	let { data, children } = $props();

	// Type assertion for data
	const summaries = (data as any).summaries || [];
</script>

<div class="layout">
	<main>
		<button onclick={() => goto('/blog')} class="mb-4 p-2 text-gray-500 rounded" aria-label="Back to Blog">
			<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
			</svg>
		</button>
		<div class="m-4">
			{@render children()}
		</div>
	</main>

	<aside>
		<h2 class="text-sm text-blue-700 cursor-pointer m-4">More posts</h2>
		<ul>
			{#each summaries as { slug, title }}
				<li>
					<a href="/blog/{slug}">{title}</a>
				</li>
			{/each}
		</ul>
	</aside>
</div>