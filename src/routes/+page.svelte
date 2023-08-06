<script>
	import Image from '$lib/Image.svelte';
</script>

<Image src="/favicon.png" alt="" let:error let:srcSet let:src>
	{#if error}
		hehe placeholder
	{:else}
		<img {src} srcset={srcSet} alt="" />
	{/if}
</Image>
