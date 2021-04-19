<template>
	<div class="app-match-player"
				:droppable="inFirstRound"
				@drop.prevent="drop"
				@dragover="dragover"
				@dragenter="dragenter"
	>
		<template v-if="!(this.player.name === '' && this.player.id === '')">
			{{player.id}}. {{player.name}}
		</template>
	</div>
</template>

<script>
export default {
	name: 'AppMatchPlayer',

	props: {
		inFirstRound: {
			type: Boolean,
			default: false,
		},

		player: {
			type: Object,
			default: () => ({
				id: '',
				name: '',
			}),
		},
	},

	methods: {
		drop(e) {
			if (!e.dataTransfer.getData('Player')) return

			const player = JSON.parse(e.dataTransfer.getData('Player'))
			this.$emit('setPlayer', player)
		},

		dragover(e) {
			if (this.inFirstRound)
				e.preventDefault()
		},
		dragenter(e) {
			if (this.inFirstRound)
				e.preventDefault()
		},
	},
}
</script>

<style>
.app-match-player {
	position: relative;
	box-sizing: border-box;

	border: 1px solid #000;
	padding: 5px;

	height: 30px;
}
</style>