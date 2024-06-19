<template>
	<ul>
		<li @click="setCrypto('BTC')" :className="cryptoNow == 'BTC' ? 'active' : ''">Bitcoin</li>
		<li @click="setCrypto('ETH')" :className="cryptoNow == 'ETH' ? 'active' : ''">ETH</li>
		<li @click="setCrypto('USDT')" :className="cryptoNow == 'USDT' ? 'active' : ''">USDT</li>
	</ul>
</template>

<script>
	export default {
		props: {
			setCrypto: {
				type: Function,
				required: true
			},
			cryptoNow: {
				type: String,
				required: true
			}
		},
	}
</script>

<style scoped>
	ul {
		margin-top: 30px;
		font-family: Montserrat;
		font-weight: 600;
		list-style: none;
		width: 200px;
		padding: 0;
		border-radius: 3px;
		border: 2px solid #fafafa;
	}
	li {
		display: block;
		background: #77608d;
		color: #fff;
		padding: 20px 0;
		transition: all 0.2s ease 0s;
	}
	li:hover, li.active {
		background: #45295c;
		cursor: pointer;
	}
</style>
