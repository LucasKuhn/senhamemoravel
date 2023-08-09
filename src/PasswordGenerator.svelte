<script>
	import { onMount } from 'svelte';

	import unidecode from 'unidecode';

	let words = [];
	let password = ' ';
	let isCopied = false;
	let shouldCapitalize = false;
	let shouldAddNumber = false;

	onMount(() => {
		fetch('/words.txt')
			.then((response) => response.text())
			.then((text) => {
				words.push(...text.split('\n'));
			});
	});

	function getRandomWord() {
		return words[Math.floor(Math.random() * words.length)];
	}

	async function generatePassword() {
		const button = this;

		button.setAttribute('aria-busy', 'true');

		await new Promise((r) => setTimeout(r, 300));

		let selected = [getRandomWord(), getRandomWord(), getRandomWord()];
		selected = selected.map((word) => unidecode(word));
		password = selected.join('-');
		capitalize();
		addNumber();
		button.removeAttribute('aria-busy');
	}

	function capitalize() {
		if (shouldCapitalize) {
			password = password
				.split('-')
				.map((word) => word.charAt(0).toUpperCase() + word.slice(1))
				.join('-');
		} else {
			password = password
				.split('-')
				.map((word) => word.charAt(0).toLowerCase() + word.slice(1))
				.join('-');
		}
	}

	function addNumber() {
		if (shouldAddNumber) {
			password = password + '-' + Math.floor(Math.random() * 10);
		} else {
			password = password.replace(/\d$/, '');
			password = password.replace(/-$/, '');
		}
	}

	async function copyPasswordToClipboard() {
		isCopied = true;
		setTimeout(() => {
			isCopied = false;
		}, 150);
		password = document.querySelector('input').value;
		navigator.clipboard.writeText(password);
	}
</script>

<article>
	<h1>Gerador de senha memorável</h1>

	<div class="mygrid">
		<div>
			<input type="text" disabled={isCopied} value={password} />
		</div>
		<div>
			<button class="secondary" on:click={copyPasswordToClipboard}>copiar</button>
		</div>
	</div>
	<button on:click={generatePassword}> Gerar </button>
	<label for="capitalize">
		<input
			id="capitalize"
			type="checkbox"
			role="switch"
			bind:checked={shouldCapitalize}
			on:change={capitalize}
		/>
		Primeira letra maiúscula
	</label>
	<label for="add_number">
		<input
			id="add_number"
			type="checkbox"
			role="switch"
			bind:checked={shouldAddNumber}
			on:change={addNumber}
		/>
		Adicionar um número
	</label>
</article>

<style>
	input[type='text'] {
		text-align: center;
	}

	.mygrid {
		display: grid;
		grid-template-columns: 1fr auto;
		grid-gap: 10px;
		align-items: center;
	}
</style>
