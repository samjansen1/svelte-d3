<script>
	let name = 'sam';
	let age = 35;

	// $: prompts Svelte to create a reactive variable
	// Whenever expression on left changes, the reactive
	// variable updates
	$: uppercaseName = name.toUpperCase();

	function increaseAge() {
		age++;
	}

	function changeName() {
		name = 'samuel'
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<!-- Single curly braces prompt Svelte to look for
	something in script block matching that name -->
<h1>Hello {uppercaseName}, my age is {age}</h1>
<!-- on: prompts Svelte to add event listener with a
	pointer to a function in the curly braces -->
<button on:click={increaseAge}>Increase Age</button>
<!-- bind: sets up two-way binding -->
<input type="text" bind:value={name}>
