<script>
	import '@picocss/pico';
</script>

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
