<template>
	<div class="chart-container">
		<b-container>
			<b-row class="justify-content-md-center">
				<b-col cols="12 text-center" md="8">
					<h1>Demo работы billboard.js</h1>
				</b-col>
			</b-row>
			
			<b-row class="justify-content-md-center">
				<b-col cols="12">
					<chart :dataArea="loadedData1" :dataLine="loadedData2" @selected="handlerClick"></chart>
				</b-col>
			</b-row>
			
			<div class="chart-actions">
				<b-row>
					<b-col cols="12" md="4">
						<div class="chart-action">
							<div class="chart-action__head">Выбранное значение:</div>
							<div class="chart-action__body">
								<b-form-input v-model="selectedValue" type="text" :disabled="true"></b-form-input>
							</div>
						</div>
					
					</b-col>
					<b-col cols="12" md="6">
						<div class="chart-action">
							<div class="chart-action__head">Обновление данных графика. По нажатию формируется новый массив из 6
								элементов (от 0 до 250) и обновляется выбранный тип графика.
							</div>
							<div class="chart-action__body">
								<b-button variant="primary" @click="updateAreaData">
									Update area
								</b-button>
								
								
								<b-button variant="primary" @click="updateLineData">
									Update line
								</b-button>
							</div>
						</div>
					</b-col>
				</b-row>
			</div>
		</b-container>
	
	
	</div>
</template>

<script>
	import Chart from './components/Chart'
	
	export default {
		components: {
			Chart
		},
		name: 'HelloWorld',
		props: {},
		data () {
			return {
				loadedData1: [],
				loadedData2: [],
				selectedValue: ''
			}
		},
		
		created () {
			this.loadedData1 = this.generateData()
			this.loadedData2 = this.generateData()
		},
		
		methods: {
			handlerClick (value) {
				this.selectedValue = value
			},
			
			updateAreaData () {
				this.loadedData1 = this.generateData()
				this.$root.$emit('updateChart')
			},
			
			updateLineData () {
				this.loadedData2 = this.generateData()
				this.$root.$emit('updateChart')
			},
			
			generateData () {
				return Array.from({length: 6}, () => Math.floor(Math.random() * 250))
			}
		}
	}
</script>

<style lang="scss">
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
	
	.chart-container {
		margin: 10vh 0;
		
		h1 {
			margin-bottom: 60px;
		}
	}
	
	.chart-actions {
		margin: 50px 0;
	}
	
	.chart-action {
		margin-bottom: 16px;
		
		&__head {
			margin-bottom: 16px;
			font-size: 16px;
		}
		
		&__body {
			display: flex;
			flex-wrap: wrap;
			
			.btn {
				margin: 0 16px 16px 0;
			}
		}
	}
</style>
