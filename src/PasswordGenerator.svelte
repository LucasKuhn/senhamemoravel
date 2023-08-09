<script>
	import { onMount } from 'svelte';
	
	import unidecode from 'unidecode';

	let words = [];
	let password = ' ';
	let isCopied = false;

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

		button.removeAttribute('aria-busy');
	}

	async function copyPasswordToClipboard() {
		isCopied = true;
		setTimeout(() => {
			isCopied = false;
		}, 150);
		// Get current password from whatever value is on the field, in case the user changed it manually
		password = document.querySelector('input').value;
		navigator.clipboard.writeText(password);
	}
</script>

<article>
	<h1>Gerador de senha memorável</h1>
	<div class="grid">
		<input type="text" disabled={isCopied} value={password}/>
		<button class="secondary" on:click={copyPasswordToClipboard}>copiar</button>
	</div>
	<button on:click={generatePassword}> Gerar </button>
</article>

<style>
	input[type='text'] {
		text-align: center;
	}

	.grid {
		display: grid;
		grid-template-columns: 1fr auto;
		grid-gap: 10px;
		align-items: center;
	}
</style>
