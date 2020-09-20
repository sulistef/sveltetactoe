<script>
	import { fade } from 'svelte/transition';

	let board = new Array(9).fill('');
	let player = 'X';
	let playable = true;
	let win = false;

	const check = (cell) => {
		if (playable) {
			if (checkEmpty(board, cell)) {
				board[cell] = player;
				checkVictory(board);
				if (checkEmptyCell(board) === false) draw();
				player === 'X' ? player = 'O' : player = 'X'
			} else {
				alert("Vous ne pouvez pas jouer sur cette case");
			}
		};
	};

	const checkEmpty = (game, cell) => { 
		if (game[cell] !== '') return false;
		else return true;
	}

	const defineClass = (val) => {
		if (val === "X") return "cross"
		else return "circle";
	};

	const checkVictory = (game) => {
		if(equality(game, 0, 1, 2)) victoire()
		else if (equality(game, 3, 4, 5)) victoire()
		else if (equality(game, 6, 7, 8)) victoire()
		else if (equality(game, 0, 3, 6)) victoire()
		else if (equality(game, 1, 4, 7)) victoire()
		else if (equality(game, 2, 5, 8)) victoire()
		else if (equality(game, 0, 4, 8)) victoire()
		else if (equality(game, 2, 4, 6)) victoire()
	};

	const equality = (game, a, b, c) =>
		(game[a] !== '' && game[b] !== '' && game[c] !== '' && game[a] === game[b] && game[b] === game[c])

	const checkEmptyCell = (game) =>
		game.map(valeur => valeur === '').includes(true);

	const victoire = () => {
		playable = false;
		win = true;
		alert("Victoire de " + player);
	};

	const draw = () => {
		alert("Egalité !");
		playable = false;
	};

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
				<div class={defineClass(board[0])} transition:fade>{@html board[0]}</div>
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