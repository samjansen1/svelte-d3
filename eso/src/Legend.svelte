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
  background-origin: border-box;
  box-shadow: 0px 0.5px 1.5px rgba(54, 122, 246, 0.25), inset 0px 0.8px 0px -0.25px rgba(255, 255, 255, 0.2);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}
</style>
