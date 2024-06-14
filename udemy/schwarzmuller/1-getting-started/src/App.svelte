<script>
	let name = 'Sam';
	let age = 35;

	function increaseAge() {
		age++;
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {name}, my age is {age}</h1>
<button on:click={increaseAge}>Increase Age</button>
