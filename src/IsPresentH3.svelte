<script>
	export let value;
</script>

{#if value}
	<h3>{String(value)}</h3>
	{:else}
	<h3>no data</h3>
	{/if}