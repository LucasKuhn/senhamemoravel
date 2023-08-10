<script>
	import PasswordGenerator from '../PasswordGenerator.svelte';
</script>

<svelte:head>
  <title>Senha memorável</title>
  <meta name="description" content="Gerador de senhas memoráveis em português do Brasil" />
</svelte:head>

<main class="container">
    <div style="width: 100%;">
	    <PasswordGenerator />
    </div>
</main>

<style>
	main {
		align-items: center;
		height: 100vh;
	}
</style>
