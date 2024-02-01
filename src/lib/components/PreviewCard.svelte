<script lang="ts">
	import * as Card from '$lib/components/ui/card';
	import type { Background } from '$lib/assets';

	const { background } = $props<{ background: Background }>();
</script>

<a href={'/' + background.id}>
	<Card.Root class="w-[300px] h-[340px] cursor-pointer hover:border-neutral-400">
		<img
			src={background.preview_img_path}
			class="rounded-t-lg"
			alt="An image of the 3d background"
		/>
		<Card.Header>
			<Card.Title>{background.name}</Card.Title>
			<Card.Description>{background.description}</Card.Description>
		</Card.Header>
	</Card.Root>
</a>
