<script>
	let password = ''
	let passwordValidity = 'short'

	$: if (password.trim().length < 5) {
		passwordValidity = 'short'
	} else if (password.trim().length > 10) {
		passwordValidity = 'long'
	} else {
		passwordValidity = 'valid'
	}

	let passwords = [];

	function addPassword() {
		if (passwordValidity === 'valid') {
			passwords = [
				...passwords,
				{
					id: Math.random(),
					password: password
				}

			]
		}
	}

	function removePassword(password) {
		passwords = passwords.filter(item => item !== password)
	}
</script>

<h1>Assignment</h1>

<p>Solve these tasks.</p>

<ol>
	<li>Add a password input field and save the user input in a variable.</li>
	<li>Output "Too short" if the password is shorter than 5 characters and "Too long" if it's longer than 10.</li>
	<li>Output the password in a paragraph tag if it's between these boundaries.</li>
	<li>Add a button and let the user add the passwords to an array.</li>
	<li>Output the array values (= passwords) in a unordered list (ul tag).</li>
	<li>Bonus: If a password is clicked, remove it from the list.</li>
</ol>

<input type="password" bind:value={password}>
<button on:click={addPassword}>Add password</button>

{#if password.length === 0}
	<p>Enter a password</p>
{:else if passwordValidity === 'short'}
	<p style='color:red'>Too short</p>
{:else if passwordValidity === 'long'}
	<p style='color:red'>Too long</p>
{:else}
	<p>{password}</p>
{/if}

<ul>
	{#each passwords as pw (pw.id)}
		<li on:click={() => removePassword(pw)}>{pw.password}</li>
	{/each}
</ul>
