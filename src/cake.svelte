<script>
	// 	Note: Due to REPL limitations, full responsiveness may not work here. Download the example from here or from the website (https://layercake.graphics/example/Bar) and run locally to get all features.
	
	import { LayerCake, Svg } from 'layercake';
	import { scaleBand } from 'd3-scale';

	import Bar from './bar.svelte';
	import AxisX from './AxisX.svelte';
	import AxisY from './AxisY.svelte';

	import data from './groups.js';

	const xKey = 'value';
	const yKey = 'year';

	data.forEach(d => {
		d[xKey] = +d[xKey];
	});
</script>



<div class="chart-container">
	<LayerCake
		padding={{ top: 0, bottom: 20, left: 35 }}
		x={xKey}
		y={yKey}
		yScale={scaleBand().paddingInner([0.05])}
		yDomain={['1979', '1980', '1981', '1982', '1983']}
		xDomain={[0, null]}
		data={data}
	>
		<Svg>
			<AxisX
				gridlines={true}
				baseline={true}
				snapTicks={true}
			/>
			<AxisY
				gridlines={true}
			/>
			<Bar/>
		</Svg>
	</LayerCake>
</div>


<style>
	/*
		The wrapper div needs to have an explicit width and height in CSS.
		It can also be a flexbox child or CSS grid element.
		The point being it needs dimensions since the <LayerCake> element will
		expand to fill it.
	*/
	.chart-container {
		width: 100%;
		height: 400px;
	}
</style>