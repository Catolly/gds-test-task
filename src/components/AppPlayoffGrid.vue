<template>
	<div class="app-playoff-grid">

		<div 
			v-for="(round, roundIndex) in roundList"
			class="round"
		>	
			<!-- children match elements -->
			<app-match
				v-for="(match, matchIndex) in round"
				:inLastRound="roundIndex===0"
				:match="match"
				class="match"
				@setPlayer="$emit('setPlayer',  [...$event, matchIndex])"
			/>
		</div>

	</div>
</template>

<script>
import AppMatch from '@/components/AppMatch'

export default {
	name: 'AppPlayoffGrid',

	components: {
		AppMatch,
	},

	props: {
		matchTree: {
			type: Object,
			required: true,
		},
	},

	computed: {
		roundList() {
			return this.treeToArray(this.matchTree) 
		},
	},

	methods: {
		treeToArray(tree, acc=[], depth=0) { 

			// init [] to accumulator[depth]
			if (!acc[depth])
				acc[depth] = [] 

			acc[depth].push(tree)

			// tree has children
			if (tree.children && tree.children.length) {
				// adding tree children to accumulator
				tree.children.map(child => {
					this.treeToArray(child, acc, depth+1)
				})
			}
			
			return acc
		},
	},
}
</script>

<style>
.app-playoff-grid {
	position: relative;

	display: flex;
	flex-direction: row-reverse;
}

.round {
	display: flex;
	flex-direction: column;

	min-width: 10%;
	width: 100%;

	justify-content: space-around;
}

.match {
	flex-grow: 1;
}

.match:not(:first-child) {
	margin-top: 30px;
}
</style>