<template>
	<div class="body-game__board board">
		<div class="board__body">
			<button 
				class="board__square"
				@click="onSquareClick(index)" 
				:key="square.id" 
				:class="{ _highlighted: square.isHighlighted }"
				v-for="(square, index) in squares" type="button"
				>
				{{ square.value }}
			</button>
		</div>
	</div>
</template>


<script>
import { mapMutations, mapGetters } from 'vuex';

export default {
	
	name: "vBoard",
	components: {
	},
	computed: mapGetters([
		'isBotTurn',
		'squares',
		'mode',
		'gameIsOver',
		'emptySquaresCount'
	]),
	methods: {
		...mapMutations([
			'calculateWinner',
			'setSquareValue',
			'botHandler',
			'toggleTurn',
			'resetGame',
			'gameOver'
		]),
		onSquareClick(index) {
			if (this.mode === 'single-player') {
				this.$store.dispatch('singlePlayerModeHandler', index);
			} else if (this.mode === 'multiplayer') {
				this.$store.dispatch('multiplayerModeHandler', index);
			}
		}
	},
}
</script>

<style lang="scss">
.board {
	display: flex;
	align-items: center;
	&__body {
		display: flex;
		flex-wrap: wrap;
		width: 240px;
	}
	&__square {
		font-size: 55px;
		height: 80px;
		flex: 0 0 80px;
		line-height: 80px;
		border: 1px solid #fff;
		margin-top: -1px;
		margin-right: -1px;
		color: inherit;
		&._highlighted {
			color: rgb(113, 241, 63);
		}
	}
}
</style>