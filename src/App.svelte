<script>
	import IsPresentH3 from "./IsPresentH3.svelte"
	import IsPresentP from "./IsPresentP.svelte"
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
	<h1>{object.cards[0].name}</h1>
	<IsPresentH3 value={object.cards[0].names} />
	<!-- svelte-ignore a11y-img-redundant-alt -->
	<img src="{object.cards[0].imageUrl}" alt="image of the card"/>
	<p>manaCost</p><IsPresentP value={object.cards[0].manaCost}/>
	<p>cmc</p><IsPresentP value={object.cards[0].cmc}/>
	<p>colors</p><IsPresentP value={object.cards[0].colors}/>
	<p>colorIdentity</p><IsPresentP value={object.cards[0].colorIdentity}/>
	<p>type</p><IsPresentP value={object.cards[0].type}/>
	<p>supertypes</p><IsPresentP value={object.cards[0].supertypes}/>
	<p>types</p><IsPresentP value={object.cards[0].types}/>
	<p>subtypes</p><IsPresentP value={object.cards[0].subtypes}/>
	<p>rarity</p><IsPresentP value={object.cards[0].rarity}/>
	<p>set</p><IsPresentP value={object.cards[0].set}/>
	<p>text</p><IsPresentP value={object.cards[0].text}/>
	<p>artist</p><IsPresentP value={object.cards[0].artist}/>
	<p>number</p><IsPresentP value={object.cards[0].number}/>
	<p>power</p><IsPresentP value={object.cards[0].power}/>
	<p>tougheness</p><IsPresentP value={object.cards[0].tougheness}/>
	<p>multiverseid</p><IsPresentP value={object.cards[0].multiverseid}/>
	<p>rulings</p><IsPresentP value={object.cards[0].rulings}/>
	<p>originalText</p><IsPresentP value={object.cards[0].originalText}/>
	<p>originalType</p><IsPresentP value={object.cards[0].originalType}/>
	<p>id</p><IsPresentP value={object.cards[0].id}/>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}