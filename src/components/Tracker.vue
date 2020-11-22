<template>
	<div class="tracker">
		<div class="container">
			<div class="rub">
				<input type="number" placeholder="Введите сумму" v-model="roubleLocal">
				<span><img src="https://www.flaticon.com/svg/static/icons/svg/153/153107.svg" alt=""></span>
			</div>

			<div class="currency" :class="{currencyAc: changedCur}" @click="changedCur = !changedCur">
				<div class="switch"></div>
				<button>$</button>
				<button>€</button>
			</div>


			<div class="res"  v-if="roubleLocal !== null">
				<h2>Итого:</h2>
				<h1>
					<span v-if="!changedCur">$</span>
					<span v-else>€</span>{{mainResult.toFixed(2)}}
				</h1>
			</div>
		</div>
	</div>
</template>

<script>
import axios from 'axios'
	export default{
		data(){
			return{
				roubleLocal: null,
				changedCur: false,
				cursUSD: {},
				cursEUR: {},

			}
		},
		computed: {
			mainResult(){
				if(!this.changedCur){
					return this.roubleLocal / this.cursUSD.Value
				}else{
					return this.roubleLocal / this.cursEUR.Value
				}
			}
		},
		created(){
			axios
			.get('https://www.cbr-xml-daily.ru/daily_json.js')
			.then(res=>{
				this.cursUSD = res.data.Valute.USD
				
				this.cursEUR = res.data.Valute.EUR
			})
		}
	}
</script>


<style>
	.currency{
		background-color: #f0f0f0;
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 15px;
		border-radius: 30px;
		position: relative;
	}
	.switch{
		position: absolute;
	    width: 50%;
	    border-radius: 24px;
	    background-color: #fff;
	    height: calc(100% - 15px);
	    z-index: 0;
	    left: 7px;
	    transition: all .3s ease;
	    top: 7px;
	}
	.currencyAc .switch{
		left:calc(50% - 7px);
	}
	.currency button{
		font-size: 30px;
		width: 45%;
		padding: 20px 0;
		font-weight: 600;
		position: relative;
		background-color: transparent;
		border: none;
	}
	.tracker{
		padding-top: 40px; 
	}
	.container{
		padding: 0 30px;
	}

	.rub{
		position: relative;
		margin-bottom: 40px;
	}
	input{
		position: relative;
		box-sizing: border-box;
		border-radius: 5px;
		border: 2px #ddd solid;
		color: #616161;
		font-size: 20px;
		font-weight: 600;
		padding: 12px;
		width: 100%!important;
		box-shadow: none!important;
	}
	input::placeholder{
		color: #b5b5b5;
	}
	.rub span{
		position: absolute;
		right: 0;
		top: 0;
		height: 50px;
		width: 50px;
		display: flex;
		align-items: center;
		font-size: 30px;
		font-weight: 400;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	img{
		height: 50%;
	}
</style>