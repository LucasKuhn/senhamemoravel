<script>
	import PasswordGenerator from '../PasswordGenerator.svelte';
</script>

<svelte:head>
	<title>Senha memorável | Gerador de senhas fortes</title>
	<meta name="description" content="Gerador de senhas fortes baseado em palavras" />
</svelte:head>

<main class="container">
	<div style="width: 100%;">
		<PasswordGenerator />
		<div />
		<article>
			<details open>
				<summary>Sobre</summary>
				<br>
				<p>
					O gerador utiliza palavras reais para compor senhas que se destacam pela facilidade de memorização. Em vez de sequências aleatórias e complexas, aproveitamos a naturalidade com que nosso cérebro lembra de palavras, garantindo senhas que são simultaneamente seguras e intuitivas para recordar.
				</p>
			</details>
			<details>
				<summary>Entenda mais</summary>
				<br>
				<p>
					Uma senha longa é frequentemente mais segura do que uma curta, e aqui está o porquê:
					imagine sua senha como uma chave. Uma chave pequena pode ser facilmente copiada ou
					adivinhada, enquanto uma chave mais longa tem mais recortes e variações, tornando-a mais
					difícil de ser replicada. No mundo digital, cada caractere adicional em sua senha aumenta
					exponencialmente o número de tentativas necessárias para que alguém a adivinhe ou quebre
					por força bruta. Assim, ao optar por uma senha mais longa, você está essencialmente
					colocando mais barreiras entre seus dados e possíveis invasores, garantindo uma proteção
					muito mais robusta.
				</p>
				<p>
					Utilizar palavras em senhas oferece uma combinação poderosa de segurança e memorabilidade.
					Primeiramente, palavras são naturalmente mais longas do que caracteres individuais, o que,
					por si só, já amplia a robustez da senha. Além disso, combinar várias palavras aleatórias
					cria uma complexidade que desafia os ataques de força bruta. Mas o verdadeiro trunfo está
					na facilidade de lembrança: nosso cérebro é programado para reconhecer e reter palavras,
					tornando-as mais fáceis de recordar do que uma sequência arbitrária de letras, números e
					símbolos. Portanto, ao usar palavras, você não apenas fortalece sua senha, mas também a
					torna mais amigável e gerenciável no dia a dia.
				</p>
			</details>
		</article>
	</div>
</main>

<style>
	main {
		align-items: center;
		height: 100vh;
	}
</style>
