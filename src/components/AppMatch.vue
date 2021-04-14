<template>
	<div class="app-match">
		<app-match-player 
			v-for="player in players"
			:id="player.id"
			:name="player.name"
			class="match-player"
		/>
	</div>
</template>

<script>
import AppMatchPlayer from '@/components/AppMatchPlayer'

export default {
	name: 'AppMatchGrid',

	components: {
		AppMatchPlayer,
	},

	props: {
		name: {
			type: String,
			default: 'Match name',
		},
		players: {
			type: Array,
			required: true,
		},
	},
}
</script>

<style>
.app-match {
	position: relative;
	
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	
	height: 150px;
}

.app-match:after {
	position: absolute;
	display: block;
	content: '';

	top: 12.5%;
	left: 100%;
	height: 75%;
	width: 10px;

	border: 1px solid red;
	border-left: none;
}
</style>