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
			<rect x="0" y="0" width="100" height="100" fill="#1b1b1b" />
		</svg>
	</div>
</div>

<style>
	.card {
		position: relative;
		width: 100%;
		height: 100%;
	}

	.card .front {
		position: absolute;
		background: #e1e2e1;
		border-radius: 5px;
		overflow: hidden;
		transform: rotateY(90deg);
		transition: all ease-in 0.2s;
		border: solid 1px #1b1b1b;
	}

	.flipped .front {
		transform: rotateY(0deg);
		transition-delay: 0.2s;
		border: solid 1px #1b1b1b;
	}

	.card .back {
		border-radius: 5px;
		overflow: hidden;
		transition: all ease-in 0.2s;
		transition-delay: 0.2s;
	}

	.flipped .back {
		transform: rotateY(90deg);
		transition-delay: 0s;
	}
</style>
