<script>
	import '@picocss/pico';

	// https://vercel.com/docs/analytics/quickstart
	import { dev } from '$app/environment';
	import { inject } from '@vercel/analytics';

	inject({ mode: dev ? 'development' : 'production' });
</script>

<svelte:head>
	<!-- Tags for URL preview -->
	<title>Senha memorável</title>
	<meta name="description" content="Gerador de senhas fortes baseado em palavras" />
	<!-- Tags for social media preview -->
	<meta property="og:title" content="Senha memorável" />
	<meta property="og:description" content="Gerador de senhas fortes baseado em palavras" />
	<meta property="og:image" content="https://senhamemoravel.com/og-image.png" />
	<meta property="og:url" content="https://senhamemoravel.com/" />
	<meta property="og:type" content="website" />
	<!-- Twitter summary card -->
	<meta name="twitter:card" content="summary" />
	<meta name="twitter:site" content="@senhamemoravel" />
	<meta name="twitter:creator" content="@lucaskuhn" />
	<meta name="twitter:title" content="Senha memorável" />
	<meta name="twitter:description" content="Gerador de senhas fortes baseado em palavras" />
	<meta name="twitter:image" content="https://senhamemoravel.com/twitter-image.png" />
	<!-- Favicon -->
	<link rel="icon" type="image/png" href="/favicon.png" />
</svelte:head>

<slot />

<style lang="scss">
	/* https://picocss.com/docs/customization.html */
	:root {
		--primary: #ff5622eb;
		--primary-hover: #f4501ea1;
		--primary-focus: rgba(244, 81, 30, 0.25);
		--primary-inverse: #fff;
	}
	/* Deep-orange (Common styles) */
	:root {
		--form-element-active-border-color: var(--primary);
		--form-element-focus-color: var(--primary-focus);
		--switch-color: var(--primary-inverse);
		--switch-checked-background-color: var(--primary);
	}
</style>
