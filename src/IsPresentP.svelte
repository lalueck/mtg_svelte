<script>
	export let value;
	export let string;
</script>

{#if value}
	{#if string !== "0"}	
		<p>{string}</p>	
	{/if}
		<p>{String(value)}</p>
	{/if}
