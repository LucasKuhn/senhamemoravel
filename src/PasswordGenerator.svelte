<script>
	import { onMount } from 'svelte';
	import unidecode from 'unidecode';
	import { animate, stagger } from 'motion';

	const name = 'Senha memorável';
	let button = null;
	let words = [];
	let password = ' ';
	let isCopied = false;
	let shouldCapitalize = true;
	let shouldAddNumber = true;
	let letters = [];
	let animation = null;

	onMount(() => {
		fetch('/words.txt')
			.then((response) => response.text())
			.then((text) => {
				words.push(...text.split('\n'));
			});
		animation = animate(
			(progress) => {
				console.log('progress', progress);

				// The innter html of each letter should be a random letter from the alphabet
				letters.forEach((letter) => {
					letter.innerHTML = String.fromCharCode(Math.floor(Math.random() * 26) + 97);
				});
				// And when the animation is done, it should be the original letter
				if (progress === 1) {
					letters.forEach((letter, i) => {
						letter.innerHTML = name.split('')[i];
					});
				}
			},
			{ duration: Infinity, easing: 'ease-out' }
		);
		generatePassword();
	});

	function getRandomWordFromList() {
		return words[Math.floor(Math.random() * words.length)];
	}

	function getRandomWord() {
		let selectedWord = getRandomWordFromList();
		if (selectedWord.length <= 7) {
			return selectedWord;
		} else {
			return getRandomWord();
		}
	}

	async function generatePassword() {
		// Store the original text in a variable
		const originalText = button.innerHTML;
		button.setAttribute('aria-busy', 'true');
		button.innerHTML = '';
		animation.play();
		password = ' ';
		await new Promise((r) => setTimeout(r, 400));
		let selected = [getRandomWord(), getRandomWord(), getRandomWord()];
		selected = selected.map((word) => unidecode(word));
		password = selected.join('-');
		capitalize();
		addNumber();
		button.innerHTML = originalText;
		button.removeAttribute('aria-busy');
		button.blur();
		animation.finish();
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
		if (password === ' ') {
			return;
		}
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
	<h1>Gerador de senha</h1>
	<h2 class="letters">
		{#each name.split('') as letter, i}
			<span bind:this={letters[i]} />
		{/each}
		&nbsp;
	</h2>

	<div class="mygrid">
		<div>
			<input type="text" disabled={isCopied} value={password} />
		</div>
		<div>
			<button class="secondary" on:click={copyPasswordToClipboard}>Copiar</button>
		</div>
	</div>
	<button on:click={generatePassword} bind:this={button}> Gerar </button>
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

	h2 {
		font-size: 1.5em;
		color: hsl(205, 10%, 50%);
		font-weight: normal;
	}

	.mygrid {
		display: grid;
		grid-template-columns: 1fr auto;
		grid-gap: 10px;
		align-items: center;
	}
	@media (max-width: 600px) {
		.mygrid {
			grid-template-columns: 1fr;
			grid-gap: 0;
		}
	}

	h1 {
		margin-bottom: 0;
	}
</style>
