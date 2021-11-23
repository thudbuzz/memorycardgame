<script>
	export let card;
	export let handleChoice;
	export let flipped;
	export let disabled;

	const handleClick = () => {
		if (!disabled) {
			handleChoice(card);
		}
	};
</script>

<div class="card">
	<div class:flipped>
		<svg class="front" viewbox="-10 -10 120 120">
			<polygon points={card.points} fill={card.color} />
		</svg>
		<svg class="back" on:click={() => handleClick(card)} viewbox="0 0 100 100">
			<rect x="0" y="0" width="100" height="100" fill="black" />
		</svg>
	</div>
</div>

<style>
	.card {
		position: relative;
	}

	.card img {
		width: 100%;
		height: 100%;
		display: block;
		border: 2px solid #fff;
		border-radius: 6px;
	}

	.card .front {
		position: absolute;
		transform: rotateY(90deg);
		transition: all ease-in 0.2s;
	}

	.flipped .front {
		transform: rotateY(0deg);
		transition-delay: 0.2s;
	}

	.card .back {
		transition: all ease-in 0.2s;
		transition-delay: 0.2s;
	}

	.flipped .back {
		transform: rotateY(90deg);
		transition-delay: 0s;
	}
</style>
