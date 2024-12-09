<script>
	import data from "./gen_mix_clean.json";
  	import LineChart from "./LineChart.svelte";
  	import StackedAreaChart from "./StackedAreaChart.svelte";
  	import Legend from "./Legend.svelte";

	const colors = {
		GENERATION: "#1f77b4",
		GAS: "#1f0b8e",
		COAL: "#5c30b1",
		NUCLEAR: "#245f10",
		WIND: "#4da82e",
		HYDRO: "#97d661",
		IMPORTS: "#8a53b2",
		BIOMASS: "#d6d461",
		SOLAR: "#e4e316",
		STORAGE: "#c17bcc",
		OTHER: "#e9a3e5"
	}

	console.log(colors['GAS'])

	let dataset = data.map(item => ({
        ...item,
        DATE: new Date(item.DATE)
    }));

	const keys = Object.keys(dataset[0]).slice(1,-1)

	$: clickedSource = null;
</script>

<h1>Great Britain's Energy Generation Mix</h1>
<h2>2009-2024</h2>
<Legend {colors} {keys} bind:clickedSource={clickedSource}/>
<StackedAreaChart data={dataset} {keys} {colors}/>
{#if (clickedSource)}
	<LineChart data={dataset} y={clickedSource} colour={colors[clickedSource]}/>
{/if}