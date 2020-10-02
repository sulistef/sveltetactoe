<script>
	import Case from './Case.svelte';
	import _ from 'lodash';

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

	const couleurFond = (valeur) => 
		_.isEmpty(valeur) ? 'grisClair' : valeur === 'X' ? 'croix' : 'rond';

</script>

<h1>Svelte Tac Toe</h1>
<h3>A {player} de jouer</h3>
	<div class="boardGame">
		<div class="boardRow">
			<div class="cell {couleurFond(board[0])}" on:click={() => check(0)}>
				<Case lacase={board[0]} />
			</div>
			<div class="cell {couleurFond(board[1])}" on:click={() => check(1)}>
				<Case lacase={board[1]} />
			</div>
			<div class="cell {couleurFond(board[2])}" on:click={() => check(2)}>
				<Case lacase={board[2]} />
			</div>
		</div>
		<div class="boardRow">
			<div class="cell {couleurFond(board[3])}" on:click={() => check(3)}>
				<Case lacase={board[3]} />
			</div>
			<div class="cell {couleurFond(board[4])}" on:click={() => check(4)}>
				<Case lacase={board[4]} />
			</div>
			<div class="cell {couleurFond(board[5])}" on:click={() => check(5)}>
				<Case lacase={board[5]} />
			</div>
		</div>
		<div class="boardRow">
			<div class="cell {couleurFond(board[6])}" on:click={() => check(6)}>
				<Case lacase={board[6]} />
			</div>
			<div class="cell {couleurFond(board[7])}" on:click={() => check(7)}>
				<Case lacase={board[7]} />
			</div>
			<div class="cell {couleurFond(board[8])}" on:click={() => check(8)}>
				<Case lacase={board[8]} />
			</div>
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
			border-radius: 5px;
			justify-content: center;
			align-items: center;
		}

		.grisClair {
			background-color: lightgrey;
		}

		.rond {
			background-color: lightsalmon;
		}

		.croix {
			background-color: lightgreen;
		}
		
	</style>