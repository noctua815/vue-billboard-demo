<template>
	<div class="chart">
		<div id="chart"></div>
	</div>
</template>

<script>
	import bb from 'billboard.js'
	import 'billboard.js/dist/billboard.min.css'
	
	export default {
		name: 'Chart',
		props: {
			dataArea: {
				type: Array
			},
			dataLine: {
				type: Array
			}
		},
		
		created() {
			this.$root.$on('updateChart', () => {
				this.generateChart()
			})
		},
		
		mounted() {
			this.generateChart()
		},
		
		beforeDestroy() {
			this.$root.$off('updateChart')
		},
		
		methods: {
			generateChart() {
				let self = this
				
				bb.generate({
					bindto: "#chart",
					data: {
						columns: [
							["area", ...this.dataArea],
							["line", ...this.dataLine]
						],
						types: {
							area: "area-spline",
							line: "line"
						},
						colors: {
							area: "red",
							line: "green"
						},
						onclick: function(d) {
							self.$emit('selected', d.value)
						}
					}
				});
			}
		}
	}
</script>

<style scoped>

</style>