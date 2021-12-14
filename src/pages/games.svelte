<script>
	import Grid from '../component/grid.svelte';
	import Button from '../component/button.svelte';

	let array = [];
	let enabled = true;
	let turn = "Your Turn";
	let retry = false;

	const dropClick = (i) => {
		if(!array[i]) {
			console.log(array);
			array[i] = 'X';
			turn = "Opponent Turn..."
			enabled = false;
			
			if(checkWin("X")) {
				turn = "You Win";
				retry = true;
				return;
			}

			setTimeout(opponentTurn, 2000)
		}
	}

	const opponentTurn = () => {
		let random = Math.floor(Math.random() * 8)

		if(array[random]) {
			return opponentTurn();
		}

		array[random] = "O";

		if(checkWin("O")) {
			turn = "Opponent Win";
			retry = true;
			return;
		}

		turn = "Your Turn"
		enabled = true
	}

	const checkWin = (character) => {
		if(array[0] == array[1] && array[0] == array[2] && array[0] == character) {
			return true;
		}

		if(array[3] == array[4] && array[3] == array[5] && array[3] == character) {
			return true;
		}		

		if(array[6] == array[7] && array[6] == array[8] && array[6] == character) {
			return true;
		}

		if(array[0] == array[4] && array[0] == array[8] && array[0] == character) {
			return true;
		}

		if(array[2] == array[4] && array[2] == array[6] && array[2] == character) {
			return true;
		}

		if(array[0] == array[3] && array[0] == array[6] && array[0] == character) {
			return true;
		}

		if(array[1] == array[4] && array[1] == array[7] && array[1] == character) {
			return true;
		}

		if(array[2] == array[5] && array[2] == array[8] && array[2] == character) {
			return true;
		}

		if(Object.values(array).length == 9) {
			turn = "Tie";
			return;
		}
	}
</script>

<div class="w-screen h-screen flex items-center justify-center">
	<div class="w-64 text-center">
		<h1 class="mb-10 text-3xl text-white">{turn}</h1>
		<div class="grid grid-cols-3 gap-1 w-full">
			{#each Array(9) as _, i}
					<Grid on:click|once={ enabled ? () => dropClick(i) : null } text="{array[i] || ""}"/>
			{/each}
		</div>
	</div>
</div>

<style>
	h1 {
		font-family: 'Bakbak One';
	}
</style>