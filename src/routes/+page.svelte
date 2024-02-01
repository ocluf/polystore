<script lang="ts">
	import { browser } from '$app/environment';
	import { assets } from '$lib/assets';
	import PreviewCard from '$lib/components/PreviewCard.svelte';
	import { Button } from '$lib/components/ui/button';
	import { Application } from '@splinetool/runtime';
	import { tick } from 'svelte';

	let app;
	let assetIndex = 0;

	if (browser) {
		loadSpline('Lv9riKy79TAjhsuJ');
	}

	function nextAsset() {
		assetIndex++;
		if (assetIndex >= assets.length) {
			assetIndex = 0;
		}
		loadSpline(assets[assetIndex].id);
	}

	async function loadSpline(id: string) {
		if (app) {
			app.stop();
		}
		await tick();
		const canvas = document.getElementById('canvas3d');
		app = new Application(canvas);
		app.load(`https://prod.spline.design/${id}/scene.splinecode`).then(() => {
			app.setGlobalEvents(true);
		});
	}
</script>

<div
	class="fixed w-screen h-screen isolate overflow-hidden bg-gray-900 px-6 py-24 sm:py-32 lg:px-8 -z-50"
>
	<div class="absolute inset-0 -z-10 bg-black h-full w-full object-cover" />
	<div
		class="hidden sm:absolute sm:-top-10 sm:right-1/2 sm:-z-10 sm:mr-10 sm:block sm:transform-gpu sm:blur-3xl"
		aria-hidden="true"
	>
		<div
			class="aspect-[1097/845] w-[68.5625rem] bg-gradient-to-tr from-[#ff4694] to-[#776fff] opacity-20"
			style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)"
		></div>
	</div>
	<div
		class="absolute -top-52 left-1/2 -z-10 -translate-x-1/2 transform-gpu blur-3xl sm:top-[-28rem] sm:ml-16 sm:translate-x-0 sm:transform-gpu"
		aria-hidden="true"
	>
		<div
			class="aspect-[1097/845] w-[68.5625rem] bg-gradient-to-tr from-[#ff4694] to-[#776fff] opacity-20"
			style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)"
		></div>
	</div>
</div>

<div class="absulote isolate overflow-hidden px-6 py-24 sm:py-32 lg:px-8">
	<div class="absolute left-5 top-5 text-gray-300 text-2xl font-bold">PolyStore</div>

	<div class="mx-auto max-w-3xl text-center">
		<h2 class="text-4xl font-bold tracking-tight text-white md:text-5xl sm:text-4xl">
			Make Your Website Fun
		</h2>
		<p class="mt-6 text-lg leading-8 text-gray-300">
			A collection of free 3D assets that you can copy paste into your website.
		</p>
	</div>
	<div class="p-5 mx-auto w-fit">
		<div class="w-[300px] h-[300px]">
			<canvas id="canvas3d"></canvas>
		</div>
	</div>
	<div class="mx-auto w-fit mt-5">
		<Button onclick={nextAsset} variant="outline">Next asset</Button>
	</div>
</div>

<div class="p-10 grid lg:grid-cols-3 xl:grid-cols-4 w-fit gap-10 mx-auto">
	{#each assets as background}
		<PreviewCard {background} />
	{/each}
</div>
