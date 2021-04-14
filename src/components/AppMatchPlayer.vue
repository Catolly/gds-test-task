<template>
	<div class="app-match-player">
		{{id}}. {{name}}
	</div>
</template>

<script>
export default {
	name: 'AppMatchPlayer',

	props: {
		id: {
			type: Number,
			required: true,
		},
		name: {
			type: String,
			required: true,
		},
	},
}
</script>

<style>
.app-match-player {
	position: relative;

	border: 1px solid #000;
	padding: 5px;
}

.app-match-player:before {
	position: absolute;
	display: block;
	content: '';

	top: 50%;
	left: -10px;
	height: 1px;
	width: 10px;

	background: red;
}
</style>