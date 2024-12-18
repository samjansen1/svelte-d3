<script>
	import data from "../data/gen_mix_clean.json";
  	import LineChart from "./LineChart.svelte";
  	import StackedAreaChart from "./StackedAreaChart.svelte";
  	import Legend from "./Legend.svelte";

	const colors = {
		GAS: "#240d53",
		COAL: "#4a1663",
		IMPORTS: "#6f2270",
		STORAGE: "#922f7c",
		OTHER: "#b63f86",
		NUCLEAR: "#245f10",
		WIND: "#4e7f12",
		HYDRO: "#7da010",
		BIOMASS: "#b1bf0e",
		SOLAR: "#ebde12",
	}

	let dataset = data.map(item => ({
        ...item,
        DATE: new Date(item.DATE)
    }));

	const keys = Object.keys(colors)

	$: clickedSource = null;
	$: hoveredSource = null;
</script>

<h1>Great Britain's Energy Generation Mix</h1>
<h2>Historic Monthly Generation Mix from Jan 2009-Nov 2024</h2>
<h3>Hover over an energy source to highlight it on the chart, click on it to generate a chart just for that source</h3>
<Legend {colors} {keys} bind:clickedSource={clickedSource} bind:hoveredSource={hoveredSource}  style='margin-bottom:1em'/>
<StackedAreaChart data={dataset} {keys} {colors} {hoveredSource}/>
{#if (clickedSource)}
	<h4>Generation from {clickedSource[0]+clickedSource.substring(1).toLowerCase()} (MWh)</h4>
	<LineChart data={dataset} y={clickedSource} colour={colors[clickedSource]}/>
{/if}