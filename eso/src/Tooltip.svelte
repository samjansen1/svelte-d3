<script>
    export let data;
    export let keys;
    export let colors;
    export let date;

    const row = data.filter((row) => row.DATE === date)
</script>

<div class=tooltip
    style="position: absolute;
    top: 400px;
    left: 200px;"
>
    {date}
</div>