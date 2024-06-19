<template>
	<div class="wrap">
		<h1>CRYPTO</h1>
		<InputCrypto :changeAmount="changeAmount" :convert="convert" :favourite="favourite" />
		<p class="err" v-if="error != ''">{{ error }}</p>
		<p class="res" v-if="result != 0">{{ result }}</p>
		<FavouriteCrypto :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs" />
		<div class="selectors">
			<SelectorCrypto :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
			<SelectorCrypto :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
		</div>
	</div>
</template>

<script>
	import InputCrypto from './components/InputCrypto.vue';
	import SelectorCrypto from './components/SelectorCrypto.vue';
	import FavouriteCrypto from './components/FavouriteCrypto.vue'
	import CryptoConvert from 'crypto-convert';

	const convert = new CryptoConvert();

	export default {
		components: { InputCrypto, SelectorCrypto, FavouriteCrypto },
		data() {
			return {
				amount: 0,
				cryptoFirst: '',
				cryptoSecond: '',
				error: '',
				result: 0,
				favs: []
			}
		},
		methods: {
			favourite() {
				if (this.cryptoFirst != this.cryptoSecond) this.favs.push({
					from: this.cryptoFirst,
					to: this.cryptoSecond
				});
			},
			getFromFavs(i) {
				this.cryptoFirst = this.favs[i].from
				this.cryptoSecond = this.favs[i].to
			},
			changeAmount(val) {
				this.amount = val
			},
			setCryptoFirst(val) {
				this.cryptoFirst = val
			},
			setCryptoSecond(val) {
				this.cryptoSecond = val
			},
			async convert() {
				this.result = 0;

				if (this.amount <= 0) {
					this.error = 'Введите число больше 0';
					return;
				} else if (this.cryptoFirst == '' || this.cryptoSecond == '') {
					this.error = 'Выберите конвертируемые валюты';
					return;
				} else if (this.cryptoFirst == this.cryptoSecond) {
					this.error = 'Выберите различные валюты';
					return;
				}
				this.error = '';

				await convert.ready();

				if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH')
					this.result = convert.BTC.ETH(this.amount);
				else if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT')
					this.result = convert.BTC.USDT(this.amount);
				else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC')
					this.result = convert.ETH.BTC(this.amount);
				else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT')
					this.result = convert.ETH.USDT(this.amount);
				else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC')
					this.result = convert.USDT.BTC(this.amount);
				else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH')
					this.result = convert.USDT.ETH(this.amount);
			}
		}
	}
</script>

<style scoped>
	.wrap {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.selectors {
		display: flex;
		justify-content: space-around;
		width: 700px;
		margin: 0 auto;
	}

	.err {
		position: absolute;
		top: 400px;
		font-size: 20px;
		font-weight: 700;
		color: #af0b0b;
	}

	.res {
		position: absolute;
		top: 380px;
		padding: 2px 30px;
		font-family: 'MuseoModerno';
		font-size: 28px;
		font-weight: 700;
		border: 2px solid #fff;
		border-radius: 3px;
		color: #45295C;
	}
</style>
