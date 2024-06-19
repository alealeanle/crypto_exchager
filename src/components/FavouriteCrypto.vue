<template>
	<h2>Варианты в избранном</h2>
	<div @click="getFromFavs(i)" v-for="(el, i) in favs" :key="i">
		<span>{{ el.from }}</span>
		<span>{{ el.to }}</span>
	</div>
</template>

<script>
	export default {
		props: {
			favs: {
				type: Array,
				required: true
			},
			getFromFavs: {
				type: Function,
				required:true
			}
		}
	}
</script>

<style scoped>
	h2 {
		margin-top: 40px;
		font-weight: 400;
		color: #fff;
	}

	div {
		display: flex;
		justify-content: space-between;
		width: 500px;
		margin: 10px auto;
		transition: all 0.3s ease 0s;
	}

	div:hover {
		opacity: .7;
		transform: scale(1.1);
		cursor: pointer;
	}

	span {
		padding: 10px 15px;
		color: #fff;
background-color: #77608d;
		border: 2px solid #45295c;
		border-radius: 5px;
	}
</style>
