<script>

    export let keys;
    export let clickedSource;
    export let hoveredSource;
    export let colors;

    const clickHandler = (event) => clickedSource = event.target.innerText
    const hoverHandler = (event) => hoveredSource = event.target.innerText
</script>

<div>
    <div>
        <p>High Carbon Sources:</p>
        {#each keys.slice(0,5) as key}
            <button class=button
                class:hovered={hoveredSource === key}
                on:click={clickHandler}
                on:mouseover={hoverHandler}
                on:mouseout={() => hoveredSource = null}
                style="background-color:{colors[key]}"
            >
                {key}
            </button>
        {/each}
    </div>
    <div>
        <p>Low/Zero Carbon Sources:</p>
        {#each keys.slice(5) as key}
            <button class=button
            class:hovered={hoveredSource === key}
            on:click={clickHandler}
            on:mouseover={hoverHandler}
            on:mouseout={() => hoveredSource = null}
            style="background-color:{colors[key]}"
        >
            {key}
        </button>
    {/each}
    </div>
</div>


<style>

/* CSS */
.button {
  align-items: center;
  padding: 6px 14px;
  font-family: -apple-system, BlinkMacSystemFont, 'Roboto', sans-serif;
  border-radius: 6px;
  border: none;
  margin-right: 0.5em;
  color: #fff;
}

.hovered {
    box-shadow: 5px 5px 10px 0 rgba(0,0,0,0.24), 5px 5px 10px 0 rgba(0,0,0,0.19);
}
</style>
