<script>
	export let value;
</script>

{#if value}
	<p>{String(value)}</p>
	{:else}
	<p>no data</p>
	{/if}
