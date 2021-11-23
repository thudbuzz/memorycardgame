<script>
	import { onMount } from 'svelte';

	import SingleCard from '$lib/SingleCard.svelte';

	const cardImages = [
		{
			description: 'square',
			color: 'blue',
			matched: false,
			points: '0,0 100,0 100,100 0,100'
		},
		{
			description: 'rectangle',
			color: 'green',
			matched: false,
			points: '0,30 100,30 100,70 0,70'
		},
		{
			description: 'triangle',
			color: 'red',
			matched: false,
			points: '50,10 100,90 0,90'
		},
		{
			description: 'shield',
			color: 'orange',
			matched: false,
			points: '0,0 100,0 100,50 50,100 0,50'
		},
		{
			description: 'diamond',
			color: 'black',
			matched: false,
			points: '50,0 100,50 50,100 0,50'
		},
		{
			description: 'cross',
			color: 'purple',
			matched: false,
			points: '30,0 70,0 70,30 100,30 100,70 70,70 70,100 30,100 30,70 0,70 0,30 30,30'
		}
	];

	$: cards = [];
	$: turns = 0;
	$: choiceOne = null;
	$: choiceTwo = null;
	$: disabled = false;

	const shuffleCards = () => {
		const shuffledCards = [...cardImages, ...cardImages]
			.sort(() => Math.random() - 0.5)
			.map((card) => ({ ...card, id: Math.random() }));

		cards = shuffledCards;
		turns = 0;
	};

	const handleChoice = (card) => {
		choiceOne ? (choiceTwo = card) : (choiceOne = card);
		if (choiceTwo && choiceTwo) {
			disabled = true;
			if (choiceOne.description === choiceTwo.description) {
				cards = cards.map((card) => {
					if (card.description === choiceOne.description) {
						return { ...card, matched: true };
					} else {
						return { ...card };
					}
				});
				resetTurn();
			} else {
				setTimeout(() => resetTurn(), 1000);
			}
		}
	};

	const resetTurn = () => {
		choiceOne = null;
		choiceTwo = null;
		turns++;
		disabled = false;
	};

	onMount(() => {
		shuffleCards();
	});
</script>

<div class="wrapper">
	<div class="header">
		<h1>Memory Card Game</h1>
		<button on:click={shuffleCards}>New Game</button>
		<p>Turns:{turns}</p>
	</div>
	<div class="card-grid">
		{#each cards as card (card.id)}
			<SingleCard
				{card}
				{handleChoice}
				flipped={card === choiceOne || card === choiceTwo || card.matched}
				{disabled}
			/>
		{/each}
	</div>

	<p>
		Made by <a href="https://www.thudbuzz.dev">Thudbuzz</a> with
		<a href="https://kit.svelte.dev/">SvelteKit</a>
	</p>
</div>

<style>
	.wrapper {
		max-width: 720px;
		margin: 0 auto;
		padding: 0 1em;
		font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial,
			sans-serif;
	}

	.header {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 1em;
	}

	h1 {
		text-align: center;
		margin-top: 1rem;
		margin-bottom: 1rem;
	}

	button {
		font-size: 1.5rem;
		padding: 1rem 2rem;
		border: none;
		border-radius: 5px;
		margin-bottom: 1rem;
	}

	p {
		text-align: center;
		font-size: 1.5rem;
	}

	.card-grid {
		margin-top: 1rem;
		margin-bottom: 1rem;
		display: grid;
		grid-template-columns: repeat(4, 1fr);
		grid-gap: 0.5em;
	}
</style>
