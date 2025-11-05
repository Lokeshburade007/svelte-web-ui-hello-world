<script>
	let { data } = $props();
</script>

<h1 class="text-2xl font-bold">{data.post.title}</h1>
<div class="text-xl text-gray-400">{@html data.post.content}</div>
