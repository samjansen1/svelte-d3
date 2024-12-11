<script>
	import data from "./gen_mix_clean.json";
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
</script>

<h1>Great Britain's Energy Generation Mix</h1>
<h2>Historic Monthly Generation Mix from Jan 2009-Oct 2024</h2>
<Legend {colors} {keys} bind:clickedSource={clickedSource} style='margin-bottom:1em'/>
<StackedAreaChart data={dataset} {keys} {colors}/>
{#if (clickedSource)}
	<h4>Generation from {clickedSource[0]+clickedSource.substring(1).toLowerCase()} (MWh)</h4>
	<LineChart data={dataset} y={clickedSource} colour={colors[clickedSource]}/>
{/if}