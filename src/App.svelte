<script>
import { bubble } from "svelte/internal";


	let board = ['', '', '', '', '', '', '', '', ''];
	let player = 'X';
	let playable = true;

	const check = (cell) => {
		if (playable) {
			board[cell] = player;
			checkVictory(board);
			player === 'X' ? player = 'O' : player = 'X'
		};
	};

	const defineClass = (val) => {
		if (val === "X") return "cross"
		else return "circle";
	};

	const checkVictory = (game) => {
		console.log(checkNotEmptyBoard(game));
		if(game[0] !== '' && game[1] !== '' && game[2] !== '' && game[0] === game[1] && game[1] === game[2]) victoire()
		else if (game[3] !== '' && game[4] !== '' && game[5] !== '' && game[3] === game[4] && game[4] === game[5]) victoire()
		else if (game[6] !== '' && game[7] !== '' && game[8] !== '' && game[6] === game[7] && game[7] === game[8]) victoire()
		else if (game[0] !== '' && game[3] !== '' && game[6] !== '' && game[0] === game[3] && game[3] === game[6]) victoire()
		else if (game[1] !== '' && game[4] !== '' && game[7] !== '' && game[1] === game[4] && game[4] === game[7]) victoire()
		else if (game[2] !== '' && game[5] !== '' && game[8] !== '' && game[2] === game[5] && game[5] === game[8]) victoire()
		else if (game[0] !== '' && game[4] !== '' && game[8] !== '' && game[0] === game[4] && game[4] === game[8]) victoire()
		else if (game[2] !== '' && game[4] !== '' && game[6] !== '' && game[2] === game[4] && game[4] === game[6]) victoire()
	};

	const checkNotEmptyBoard = (game) =>
		game.map(valeur => valeur !== '').includes(true)

	const victoire = () => {
		alert("Victoire de " + player);
		playable = false;
	}

	const resetGame = () => {
		board = ['', '', '', '', '', '', '', '', ''];
		playable= true;
		player = 'X';
};
		

</script>

<h1>Svelte Tac Toe</h1>
<h3>A {player} de jouer</h3>
	<div class="boardGame">
		<div class="boardRow">
			<div class="cell" on:click={() => check(0)}>
				<div class={defineClass(board[0])}>{board[0]}</div>
			</div>
			<div class="cell" on:click={() => check(1)}>
				<div class={defineClass(board[1])}>{board[1]}</div>
			</div>
			<div class="cell" on:click={() => check(2)}>
				<div class={defineClass(board[2])}>{board[2]}</div>
			</div>
		</div>
		<div class="boardRow">
			<div class="cell" on:click={() => check(3)}><div class={defineClass(board[3])}>{board[3]}</div></div>
			<div class="cell" on:click={() => check(4)}><div class={defineClass(board[4])}>{board[4]}</div></div>
			<div class="cell" on:click={() => check(5)}><div class={defineClass(board[5])}>{board[5]}</div></div>
		</div>
		<div class="boardRow">
			<div class="cell" on:click={() => check(6)}><div class={defineClass(board[6])}>{board[6]}</div></div>
			<div class="cell" on:click={() => check(7)}><div class={defineClass(board[7])}>{board[7]}</div></div>
			<div class="cell" on:click={() => check(8)}><div class={defineClass(board[8])}>{board[8]}</div></div>
		</div>
	</div>
	<button on:click={() => resetGame()}>Redémarrer</button>

	<style>
		.boardGame {
			width: 200px;
			height: 200px;
			display: flex;
			flex-direction: column;
		}

		.boardRow {
			flex: 1;
			display: flex;
			flex-direction: row;
		}

		.cell {
			flex: 1;
			display: flex;
			margin: 3px;
			background-color: lightgrey;
			border-radius: 5px;
			justify-content: center;
			align-items: center;
		}

		.circle {
			font-size: 36px;
			font-weight: 700;
			color: brown;
		}

		.cross {
			font-size: 36px;
			font-weight: 700;
			color: green;
		}
	
	
	</style>