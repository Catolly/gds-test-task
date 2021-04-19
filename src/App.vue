<template>
	<div id='app'>
		<label>
			Bracket size: 
			<input 
				type="number"
				v-model.number="playoffGridSize"
			>
		</label>

		<app-playoff-grid
			v-if="matchTree"
			:matchTree="matchTree"
			class="playoff-grid"
			@setPlayer="setPlayer"
		/>
	</div>
</template>

<script>
import AppPlayoffGrid from '@/components/AppPlayoffGrid'

export default {
  name: 'App',

  components: {
  	AppPlayoffGrid,
  },

  data: () => ({
		playoffGridSize: 8,
		validPlayoffGridSize: 8,
		playerList: [],
	}),

	computed: {
		matchTree() {
			// if (this.playerList.slice()) 

			return this.generateMatchTree(this.validPlayoffGridSize, 
																		this.normailize(this.playerList).slice())
		},
	},

	watch: {
		playoffGridSize() {
			if (this.isValidPlayoffGridSize())
				this.validPlayoffGridSize = this.playoffGridSize
		},

		validPlayoffGridSize() {
			this.playerList = []
		},

		playerList() {
			this.playerList = this.normailize(this.playerList, 
																				this.validPlayoffGridSize)
		},
	},

	methods: {
		normailize(array, size) {
			if (!array) return new Array(size).fill({})

			if (array.length < size) {
				const sizeDifference = size - array.length

				return array.concat(new Array(sizeDifference))
										.fill({}, sizeDifference)
			}

			return array
		},

		setPlayer(e) {
			const [player, matchPlayerIndex, matchIndex] = [...e]
			this.playerList.splice(matchPlayerIndex+matchIndex*2, 1, player)
			console.log(player, matchPlayerIndex, matchIndex)
			console.log(this.playerList)
		},

		isValidPlayoffGridSize() {
			return this.playoffGridSize >= 2 && Number.isInteger(
				this.sizeToRound(this.playoffGridSize)
			)
		},

		sizeToRound(size) {
			return Math.log2(size)
		},

		generateMatchTree(size, playerList) {
			const children = Array(2).fill({})

			const maxRound = this.sizeToRound(this.validPlayoffGridSize)
			const round = this.sizeToRound(size)

			// forEach doesn't work with child, because child is empty object
			children.forEach((child, index) => children[index] = { 
				'round': round,
				'name': '',
				'players': [
					{
						'name': '',
						'id': '',
					},
					{
						'name': '',
						'id': '',
					},
				],
				children: round > 1 ? this.generateMatchTree(size/2, playerList) : []
			})
			
			if (round === 1 && playerList.length != 0)
				children.forEach((child, index) =>
					child.players = playerList.splice(0, 2)
				)

			return round != maxRound? children : children[0] // children[0] - root tree
		},

		dragstart(e, player) {
			e.dataTransfer.dropEffect = 'move'
			e.dataTransfer.effectAllowed = 'move'
			e.dataTransfer.setData('Player', JSON.stringify(player));
		},

		distributeRandom(playerList) {
			this.playerList = playerList
		},
	},

	created() {
		this.playerList = this.normailize(this.playerList, 
																			this.validPlayoffGridSize)
	},
}
</script>

<style>
.playoff-grid,
.player-list {
	margin-top: 30px;
}
</style>
