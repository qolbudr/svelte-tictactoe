<script>
	import Button from "../component/button.svelte";
	import { url } from "@roxi/routify";
	const navigate = () => {
		window.location = $url('games')
	}
</script>

<div class="w-screen h-screen m-0 p-0 flex items-center text-center overflow-hidden">
	<div class="w-full overflow-hidden">
		<h1 class="text-white text-4xl font-bold">TIC TAC TOE</h1>
		<div class="mt-10">
			<Button on:click={navigate}>Start</Button>
		</div>
	</div>
	<h1 class="text-black font-bold absolute -top-40 -left-12 m-0 p-0 corner-decor">X</h1>
	<h1 class="text-black font-bold absolute -bottom-48 -right-12 m-0 p-0 corner-decor">O</h1>
</div>

<style>
	h1 {
		font-family: 'Bakbak One';
	}

	.corner-decor {
		font-size: 20rem;
	}
</style>