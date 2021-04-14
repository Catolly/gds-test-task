<template>
	<div class="app-playoff-grid">
		<app-round
			:match-list="matchList"
			class="round"
		/>
	</div>
</template>

<script>
import AppRound from '@/components/AppRound'

export default {
	name: 'AppPlayoffGrid',

	components: {
		AppRound,
	},

	props: {
		matchList: {
			type: Array,
			required: true,
		},
	},
}
</script>

<style>
.app-playoff-grid {

}

.round {
	max-width: 20%;
	min-width: 50%;
}
</style>