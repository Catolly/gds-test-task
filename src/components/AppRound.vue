<template>
	<div class="app-round">
		<app-match 
			v-for="match in matchList"
			:name="match.name"
			:players="match.players"
			class="match"
		/>
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
		matchList: {
			type: Array,
			required: true,
		},
	},
}
</script>

<style>
.app-round {
	display: flex;
	flex-direction: column;
}
</style>