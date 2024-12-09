<script>

    export let keys;
    export let clickedSource;
    export let colors;

    const clickHandler = (event) => clickedSource = event.target.getAttribute('source');
</script>

<svg width=900 height=15>
    {#each keys as key, i}
        <g transform="translate({10+i*75}, 10)"
            on:click={clickHandler}
        >
            <rect source={key} width="10" height="10" x=0 y=-5 fill={colors[key]}/>
            <text source={key} font-size="10" x=15 text-anchor="left" dominant-baseline="middle">{key}</text>
        </g>
    {/each}
</svg>