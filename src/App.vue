<template>
  <div class="hello">
    <b-container>
      <b-row class="justify-content-md-center">
        <b-col cols="8">
          <h1>Demo работы billboard.js</h1>
        </b-col>
      </b-row>
      
      <b-row class="justify-content-md-center">
        <b-col cols="12">
          <chart :dataArea="loadedData1" :dataLine="loadedData2" @selected="handlerClick"></chart>
        </b-col>
      </b-row>
      
      
      <b-row>
        <b-col cols="4">
          <b-form-input v-model="selectedValue"
                        type="text"
                        :disabled="true"></b-form-input>
        </b-col>
        <b-col cols="4">
          <b-button variant="primary" @click="updateAreaData">
            Update area data
          </b-button>
        </b-col>
        <b-col cols="4">
          <b-button variant="primary" @click="updateLineData">
            Update line data
          </b-button>
        </b-col>
      </b-row>
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
				loadedData1: [30, 200, 100, 170, 150, 250],
				loadedData2: [130, 100, 140, 35, 110, 50],
				selectedValue: ''
			}
		},
		methods: {
			handlerClick(value) {
				this.selectedValue = value
			},
			
			updateAreaData() {
				console.log(1)
				console.log(this.generateData())
				this.loadedData1 = this.generateData()
        this.$root.$emit('updateChart')
			},
			
			updateLineData() {
				console.log(2)
				this.loadedData2 = this.generateData()
				this.$root.$emit('updateChart')
			},
			
			generateData() {
				return Array.from({length: 6}, () => Math.floor(Math.random() * 200))
			}
		}
	}
</script>

<style>
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
  }
</style>
