<script>
    export let data;
    export let keys;
    // export let colors;
    export let xScale;
    export let tooltipEvent;
    export let x;
    export let y;

    function convertToFirstDayOfMonth(timestamp) {
      // Parse the input timestamp into a Date object
      const date = new Date(timestamp);
      
      // Extract the year and month
      const year = date.getFullYear();
      const month = String(date.getMonth() + 1).padStart(2, '0'); // Add 1 to month as it's zero-based
        
      // Construct the first day of the month in ISO format
      const firstDayOfMonth = `${year}-${month}-01T00:00:00.000`;
        
       return firstDayOfMonth;
    }

    function formatDate(timestamp) {
        const date = new Date(timestamp);
        const formatter = Intl.DateTimeFormat('en-GB', { month: 'long', year: 'numeric' });
        const formattedDate = formatter.format(date);

        return formattedDate;
    }


    $:tooltipDate = convertToFirstDayOfMonth(xScale.invert(tooltipEvent.offsetX))
    $:row = data.filter((row) => row.DATE.getTime() === new Date(tooltipDate).getTime())
    $:style = `left: ${x}px; top: ${y}px`

</script>

<div class=tooltip
        style={style}
    >
        <h4>{formatDate(row[0].DATE)}</h4>
        {#each keys as key}
            <p>{key}: {row[0][key]}</p>
        {/each}
</div>

<style>
    .tooltip {
        position: absolute; 
        background: white;
        box-shadow: rgba(0, 0, 0, 0.15) 2px 3px 8px; /* Gives a nice 3d effect */
        padding: 8px 6px; /* Adds space around content within tooltip */
        border-radius: 3px; /* Rounds corners */
        pointer-events: none; /* Prevents tooltip from blocking mouse events */
        font-size: small;
    }
</style>
