<script>
	export let value;
	export let string;
</script>

{#if value}
	<p>{string}</p>	
	<p>{JSON.stringify(value)}</p>
	{/if}
