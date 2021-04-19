<template>
	<div class="app-players-list">
		Список игроков:

		<button 
			@click="distributeRandom"
		>
			Распределить случайно
		</button>

		<div class="players-list">
			<div 
				v-for="player in playerList"
				class="player"
				draggable
				@dragstart="dragstart($event, player)"
			>
				{{player.id}}. {{player.name}}
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'AppPlayersList',

	data:() => ({
		playerList: [],
	}),

	props: {
		size: Number,
	},

	watch: {
		size() {
			this.playerList = this.generatePlayerList()
		},
	},

	methods: {
		dragstart(e, player) {
			this.$emit('dragstart', e, player)
		},

		distributeRandom() {
			this.$emit('distributeRandom', this.shuffle(this.playerList).slice())
		},

		shuffle(array) {
			for (let i = array.length - 1; i > 0; i--) {
				const j = Math.floor(Math.random() * (i + 1));
				[array[i], array[j]] = [array[j], array[i]]
			}
			return array
		},

		generatePlayerList() {
			const playerList = new Array(this.size).fill({})

			playerList.forEach((player, index) => playerList[index] = {
				'id': index,
				'name': 'player ' + index
			})

			return playerList
		},
	},

	created() {
		this.playerList = this.generatePlayerList()
	},
}
</script>

<style scoped>
.player {
	border: 1px solid #000;
	padding: 5px;
	margin-top: 12px;

	width: 25%;
}
</style>