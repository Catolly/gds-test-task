<template>
	<div id='app'>
		<app-playoff-grid
			:matchList="matchList"
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
  	matchList: [
  		{
	  		name: 'Match 3',
	  		players: [
		  		{
		  			id: 1,
		  			name: "player 1",
		  		},
		  		{
		  			id: 3,
		  			name: "player 3",
		  		},
	  		],
				// children: [
				// 	{
				// 		name: 'Match 2',
				// 		players: [
				// 			{
				// 				id: 3,
				// 				name: "player 4",
				// 			},
				// 			{
				// 				id: 4,
				// 				name: "player 4",
				// 			},
				// 		],
				// 		children: [],
				// 	},
				// 	{
				// 		name: 'Match 1',
				// 		players: [
				// 			{
				// 				id: 1,
				// 				name: "player 1",
				// 			},
				// 			{
				// 				id: 2,
				// 				name: "player 2",
				// 			},
				// 		],
				// 		children: [],
				// 	}
				// ],
			},
		],
	}),
}
</script>

<style>

</style>
