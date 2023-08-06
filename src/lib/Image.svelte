<script lang="ts">
	import { DEV } from 'esm-env';
	import { onMount } from 'svelte';

	export let src: string;
	export let alt: string;

	export let formats: string[] = ['webp', 'png', 'jpg'];
	export let widths: string[] | null = null;

	export let figcaption: string | null = null;
	export let loading: 'lazy' | 'eager' = 'lazy';

	export let figureClasses: string = '';
	export let imgClasses: string = '';

	let fileName: string;
	$: if (src) {
		fileName = src.split('.')[0];
	}

	function buildSrcset() {
		if (DEV) return;
		if (src?.split('.')[1] === 'svg') return;

		let srcset = '';

		if (widths) {
			for (let i = 0; i < widths.length; i++) {
				srcset += `${fileName}-${widths[i]}.${formats[0]} ${widths[i]}w`;

				if (i < widths.length - 1) {
					srcset += ', ';
				}
			}
		} else {
			for (let i = 0; i < formats.length; i++) {
				srcset += `${fileName}.${formats[i]}`;

				if (i < formats.length - 1) {
					srcset += ', ';
				}
			}
		}

		return srcset;
	}

	let srcSet: string | undefined = undefined;

	onMount(() => {
		srcSet = buildSrcset();
	});
</script>

<slot {srcSet}>
	<figure class={figureClasses}>
		<img class={imgClasses} srcset={srcSet} {src} {alt} {loading} decoding="async" />

		{#if figcaption}
			<p>{figcaption}</p>
		{/if}
	</figure>
</slot>
