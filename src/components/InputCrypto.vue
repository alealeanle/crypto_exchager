<template>
	<input min="0" type="number" @input="changeAmount($event.target.value)" placeholder="Введите число"><br>
	<button @click="convert()">Конвертировать</button>
	<button class="fav" @click="favourite()">В избранное</button>
</template>

<script>
	export default {
		props: {
			changeAmount: {
				type: Function,
				required: true
			},
			convert: {
				type: Function,
				required: true
			},
			favourite: {
				type: Function,
				required: true
			},
		}
	}
</script>

<style scoped>
	input {
		position: relative;
		top: -50px;
		width: 500px;
		margin-bottom: 60px;
		padding: 10px 15px;
		font-size: 1.2em;
		border: 0;
		border-radius: 3px;
		color: #794f45;
		background: #fafafa;
		outline: none;
	}

	button {
		position: absolute;
		top: 345px;
		padding: 15px 20px;
		font-weight: 700;
		color: #fff;
		background-color: rgba(69, 41, 92, 0.8);
		border: 2px solid #fff;
		border-radius: 3px;
		text-transform: uppercase;
		cursor: pointer;
		transition: all 0.3s ease 0s;
	}

	button:hover {
		transform: scale(1.1);
	}

	.fav {
		top: 350px;
		left: 1080px;
		padding: 10px 20px;
	}
</style>
