<script>
	import ContactCard from "./ContactCard.svelte";

	let name = 'Sam Jansen';
	let age = 35;
	let jobTitle = "Lead Data Analyst";
	let jobDescription = "Will viz for food";
	let image;

	// $: prompts Svelte to create a reactive variable
	// Whenever expression on left changes, the reactive
	// variable updates
	$: uppercaseName = name.toUpperCase();

	function increaseAge() {
		age++;
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
<input type="text" placeholder="Job Title" bind:value={jobTitle}>
<input type="text" placeholder="Image URL" bind:value={image}>
<textarea rows=3 placeholder="Job Description" bind:value={jobDescription}></textarea>

<!-- Link prop names to variables to set them -->
<ContactCard
	userName={name} 
	{jobTitle} 
	{jobDescription} 
	{image}
/>