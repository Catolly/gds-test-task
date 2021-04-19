<template>
	<div class="app-match"
		:droppable="inFirstRound"
		@drop.stop
	>

		<div 
			v-if="match.players.length"
			class="match-players"
		>
			<app-match-player 
				v-for="(player, index) in match.players"
				:key="index"
				:player="player"
				:class="{'in-first-round': inFirstRound}"
				:inFirstRound="inFirstRound"
				class="match-player"
				@setPlayer="$emit('setPlayer', [$event, index])"
			/>
		</div>
	
		<app-match-player
			v-if="inLastRound"
			:class="{'match-empty': !match.players.length}"
			class="match-winner"
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
		inLastRound: {
			type: Boolean,
			default: false,
		},

		match: {
			type: Object,
			required: true,
		},
	},

	computed: {
		inFirstRound() {
			return this.match.round === 1
		},
	},
}
</script>

<style scoped>
.app-match {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.match-players,
.match-winner {
	flex-grow: 1;
}

.match-players {
	margin-right: 10px;
}

.match-winner {
	margin-left: 10px;
}

.match-players {
	position: relative;
	
	display: flex;
	flex-direction: column;
	justify-content: space-around;

	height: 100%;
}

.match-players:after {
	position: absolute;
	display: block;
	content: '';

	top: calc(25% - 10px);
	bottom: calc(25% - 10px);
	left: 100%;
	width: 10px;

	border: 1px solid red;
	border-left: none;
}

.match-player {
	position: relative;
	margin-left: 10px;
}

.match-player:last-child {
	margin-top: 30px;
}

.match-player.in-first-round:before {
	display: none;
}

.match-player:before,
.match-winner:before {
	position: absolute;
	display: block;
	content: '';

	top: 50%;
	left: -10px;
	height: 1px;
	width: 10px;

	background: red;
}

.match-winner.match-empty:before {
	display: none;
}
</style>