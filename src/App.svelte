<script>
	const getCard = async () => {
		var response = await fetch('https://api.magicthegathering.io/v1/cards/386616');
		var result = await response.json();
		return result;
	}

	let cardPromise = getCard();
</script>

{#await cardPromise}
	<p>...waiting</p>
{:then object}
	<p>{JSON.stringify(object.card.name)}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}