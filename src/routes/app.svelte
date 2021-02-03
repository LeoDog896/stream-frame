<h1>Test</h1>
<script lang="ts">

	import { onMount } from 'svelte';
	
	let canvas: HTMLCanvasElement;
	let context: CanvasRenderingContext2D;

	onMount(() => context = canvas.getContext('2d'))

	function render(e) {
		const reader = new FileReader()
		reader.readAsDataURL(e.target.files[0]);
		reader.onload = function(event){
			const img = new Image();
			img.src = event.target.result as string;
			img.onload = function(){
				canvas.width = img.width;
				canvas.height = img.height;
				context.drawImage(img, 0, 0);
			}
		}
	}
</script>

<input type="file"
	id="avatar" name="avatar"
	accept="image/png, image/jpeg"
	on:change={render}>

<canvas bind:this={canvas}/>