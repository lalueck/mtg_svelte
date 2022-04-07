<script>
	const getCard = async () => {
		var response = await fetch('https://api.magicthegathering.io/v1/cards?random=true&pageSize=01&contains=imageUrl&layout=normal');
		var result = await response.json();
		return result;
	}

	let cardPromise = getCard();
</script>

{#await cardPromise}
	<p>...waiting</p>
{:then object}
	<p>{JSON.stringify(object.cards[0].name)}</p>
	<!-- svelte-ignore a11y-img-redundant-alt -->
	<img src="{object.cards[0].imageUrl}" alt="image of the card"/>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}