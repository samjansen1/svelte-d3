<script>
    export let courseGoal
</script>

<style>
    .highlight {
      color: red;
    }
</style>

<h1 class:highlight={courseGoal.includes('!')}>{courseGoal}</h1>