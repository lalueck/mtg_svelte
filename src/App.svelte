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


<center>

{#await cardPromise}
	<p>...waiting</p>
{:then object}
	<h1>{object.cards[0].name}</h1>
	<IsPresentH3 value={object.cards[0].names} />
	<!-- svelte-ignore a11y-img-redundant-alt -->
	<img src="{object.cards[0].imageUrl}" alt="image of the card"/>

	<!-- ausklappbar -->
	<p>Text</p><IsPresentP value={object.cards[0].text}/>
	{#if object.cards[0].types[0] == "Creature"}
		<p>Power</p><IsPresentP value={object.cards[0].power}/>
		<p>Toughness</p><IsPresentP value={object.cards[0].toughness}/>
	{/if}

	<div class="accordion" id="accordionPanelsStayOpenExample">
		<div class="accordion-item">
		  <h2 class="accordion-header" id="panelsStayOpen-headingOne">
			<button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseOne" aria-expanded="true" aria-controls="panelsStayOpen-collapseOne">
			  Mana and colours
			</button>
		  </h2>
		  <div id="panelsStayOpen-collapseOne" class="accordion-collapse collapse" aria-labelledby="panelsStayOpen-headingOne">
			<div class="accordion-body">
				<p>Mana Cost</p><IsPresentP value={object.cards[0].manaCost}/>
				<p>cmc</p><IsPresentP value={object.cards[0].cmc}/>
				<p>Colors</p><IsPresentP value={object.cards[0].colors}/>
				<p>Color Identity</p><IsPresentP value={object.cards[0].colorIdentity}/>
			</div>
		  </div>
		</div>
		<div class="accordion-item">
		  <h2 class="accordion-header" id="panelsStayOpen-headingTwo">
			<button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseTwo" aria-expanded="false" aria-controls="panelsStayOpen-collapseTwo">
			  Type, Types and more
			</button>
		  </h2>
		  <div id="panelsStayOpen-collapseTwo" class="accordion-collapse collapse" aria-labelledby="panelsStayOpen-headingTwo">
			<div class="accordion-body">
				<p>Type</p><IsPresentP value={object.cards[0].type}/>
				<p>Supertypes</p><IsPresentP value={object.cards[0].supertypes}/>
				<p>Types</p><IsPresentP value={object.cards[0].types}/>
				<p>Subtypes</p><IsPresentP value={object.cards[0].subtypes}/>
			</div>
		  </div>
		</div>
		<div class="accordion-item">
		  <h2 class="accordion-header" id="panelsStayOpen-headingThree">
			<button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseThree" aria-expanded="false" aria-controls="panelsStayOpen-collapseThree">
			  Misc info
			</button>
		  </h2>
		  <div id="panelsStayOpen-collapseThree" class="accordion-collapse collapse" aria-labelledby="panelsStayOpen-headingThree">
			<div class="accordion-body">
				<p>Rarity</p><IsPresentP value={object.cards[0].rarity}/>
				<p>Set</p><IsPresentP value={object.cards[0].set}/>
				<p>Artist</p><IsPresentP value={object.cards[0].artist}/>
				<p>Number</p><IsPresentP value={object.cards[0].number}/>
				<p>Multiverseid</p><IsPresentP value={object.cards[0].multiverseid}/>
				<p>ID</p><IsPresentP value={object.cards[0].id}/>
			</div>
		  </div>
		</div>
		<div class="accordion-item">
			<h2 class="accordion-header" id="panelsStayOpen-headingFour">
			  <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseFour" aria-expanded="false" aria-controls="panelsStayOpen-collapseFour">
				Historic info
			  </button>
			</h2>
			<div id="panelsStayOpen-collapseFour" class="accordion-collapse collapse" aria-labelledby="panelsStayOpen-headingFour">
			  <div class="accordion-body">
				<p>Rulings</p><IsPresentP value={object.cards[0].rulings}/>
				<p>Original Text</p><IsPresentP value={object.cards[0].originalText}/>
				<p>Original Type</p><IsPresentP value={object.cards[0].originalType}/>
			  </div>
			</div>
		  </div>
	  </div>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
</center>