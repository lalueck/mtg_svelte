<script>
	export let value;
</script>

{#if value}
	<h3>{String(value)}</h3>
	{/if}