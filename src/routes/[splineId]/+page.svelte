<script lang="ts">
	import { browser } from '$app/environment';
	import { Button } from '$lib/components/ui/button';
	import { Application } from '@splinetool/runtime';
	import { tick } from 'svelte';
	import * as Dialog from '$lib/components/ui/dialog';

	let app;

	const { data } = $props();

	if (browser) {
		loadSpline();
	}

	// a function that downloads the file at https://prod.spline.design/${data.id}/scene.splinecode
	// and saves it to the user's computer
	function downloadScene(id: string) {
		fetch(`https://prod.spline.design/${data.id}/scene.splinecode`)
			.then((response) => response.blob())
			.then((blob) => {
				const url = window.URL.createObjectURL(blob);
				const link = document.createElement('a');
				link.href = url;
				link.download = 'scene.splinecode';
				link.click();
				window.URL.revokeObjectURL(url);
			});
	}

	async function loadSpline() {
		await tick();
		const canvas = document.getElementById('canvas3d');
		app = new Application(canvas);

		app.load(`https://prod.spline.design/${data.id}/scene.splinecode`).then(() => {
			app.setGlobalEvents(true);
		});
	}
</script>

<Dialog.Root>
	<Dialog.Trigger>
		<Button class="m-5">Download scene</Button>
	</Dialog.Trigger>
	<Dialog.Content>
		<Dialog.Header>
			<Dialog.Title>Download scene file</Dialog.Title>
			<Dialog.Description>
				First download the scene file. Then use on the following code snippets to integrate the
				scene into your website
				<h4 class="scroll-m-10 font-semibold text-primary mt-10 mb-2">vanilla js</h4>
				<div class="w-[470px]">
					<div
						style="background: #000000; overflow:auto;width:auto"
						class="rounded-xl scrollbar-hide p-3"
					>
						<pre style="margin: 0; line-height: 125%"><span style="color: #0000ff">import</span
							> &#123;Application&#125; from <span style="color: #a31515"
								>&#39;@splinetool/runtime&#39;</span
							>;

								
<span style="color: #0000ff">const</span> canvas = document.getElementById(<span
								style="color: #a31515">&#39;canvas3d&#39;</span
							>);
<span style="color: #0000ff">const</span> app = <span style="color: #0000ff">new</span
							> Application(canvas);
app.load(<span style="color: #a31515">&#39;https://WHERE_YOU_HOST_THE_SCENE_FILE&#39;</span>);
	
</pre>
					</div>
					<h4 class="scroll-m-10 font-semibold text-primary mt-10 mb-2">React</h4>
					<div
						style="background:  #000000; overflow:auto;width:auto;"
						class="p-3 scrollbar-hide rounded-xl"
					>
						<!-- HTML generated using hilite.me -->

						<pre style="margin: 0; line-height: 125%"><span style="color: #0000ff">import</span
							> Spline from <span style="color: #a31515">&#39;@splinetool/react-spline&#39;</span>;

<span style="color: #0000ff">export</span> <span style="color: #0000ff">default</span> <span
								style="color: #0000ff">function</span
							> App() &#123;
	<span style="color: #0000ff">return</span> (
	  &lt;Spline scene=<span style="color: #a31515">&quot;https://WHERE_YOU_HOST_THE_SCENE_FILE&;</span
							> /&gt;
	);
	&#125;
  </pre>
					</div>
				</div></Dialog.Description
			>
		</Dialog.Header>
		<Button variant="primary" class="mt-10" onclick={() => downloadScene(data.id)}
			>Download scene</Button
		>
	</Dialog.Content>
</Dialog.Root>

<div class="fixed -z-50 inset-0 flex items-center justify-center">
	<canvas id="canvas3d"></canvas>
</div>

<!-- <div
	style="background: #ffffff; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"
>
	<pre style="margin: 0; line-height: 125%"><span style="color: #008800; font-weight: bold"
			>import</span
		> &#123 Application &#125 from <span style="background-color: #fff0f0"
			>&#39;@splinetool/runtime&#39;</span
		>;

	<span style="color: #008800; font-weight: bold">const</span> canvas <span style="color: #333333"
			>=</span
		> <span style="color: #007020">document</span>.getElementById(<span
			style="background-color: #fff0f0">&#39;canvas3d&#39;</span
		>);
	<span style="color: #008800; font-weight: bold">const</span> app <span style="color: #333333"
			>=</span
		> <span style="color: #008800; font-weight: bold">new</span> Application(canvas);
	app.load(<span style="background-color: #fff0f0"
			>&#39;https://prod.spline.design/GHZot8q7hbjmkexr/scene.splinecode&#39;</span
		>);
	</pre>
</div> -->
