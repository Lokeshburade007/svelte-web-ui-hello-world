<script lang="ts">
    let { data } = $props();
</script>

<h1 class="text-xl font-bold p-4">Blog</h1>

<ul class="px-4">
    {#each data.summaries as { slug, title }}
        <li class="text-gray-600 underline"><a href="/blog/{slug}">{title}</a></li>
    {/each}
</ul>
