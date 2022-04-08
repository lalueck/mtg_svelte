<script>
	
	import IsPresentH3 from "./IsPresentH3.svelte"
	import IsPresentP from "./IsPresentP.svelte"
	let	cardPromise = null
	let searchQarry = null
	let inProgress = null
	async function getCard(userInput){
		var response = await fetch('https://api.magicthegathering.io/v1' + userInput);
		var result = await response.json();
		return result;
	}
	function loadCard(userInput){
		cardPromise = getCard(userInput);
		inProgress = true;
		cardPromise.then(() => {
			inProgress = false;
		})
	}
	// function enableButton(){
	// 	inProgress = false;
	// 	return "";
	// }
</script>

<!-- TODO: fix search and random working at once -->

<center>
	<input bind:value={searchQarry}>
	<button disabled={inProgress} on:click={()=>{loadCard(`/cards?pageSize=01&contains=imageUrl&layout=normal&name="${searchQarry}"`)}}>
		Search for card
	</button>
	<button disabled={inProgress} on:click={()=>{loadCard("/cards?random=true&pageSize=01&contains=imageUrl&layout=normal")}}>
		Random Card
	</button>
{#if cardPromise}
	{#await cardPromise}
	<p>...waiting</p>
	{:then object}
	<!-- {enableButton()} -->
	<h1>{object.cards[0].name}</h1>
	<IsPresentH3 value={object.cards[0].names} />
	<!-- svelte-ignore a11y-img-redundant-alt -->
	<img src="{object.cards[0].imageUrl}" alt="image of the card"/>

	<!-- ausklappbar -->
	<IsPresentP value={object.cards[0].text} string="Text"/>
	<i><IsPresentP value={object.cards[0].flavor} string="0"/></i>
	{#if object.cards[0].types[0] == "Creature"}
		<IsPresentP value={object.cards[0].power} string="Power"/>
		<IsPresentP value={object.cards[0].toughness} string="Toughness"/>
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
				<IsPresentP value={object.cards[0].manaCost} string="Mana Cost"/>
				<IsPresentP value={object.cards[0].cmc} string="Total mana cost"/>
				<IsPresentP value={object.cards[0].colors} string="Colours"/>
				<IsPresentP value={object.cards[0].colorIdentity} string="Colour Identity"/>
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
				<IsPresentP value={object.cards[0].type} string="Type"/>
				<IsPresentP value={object.cards[0].supertypes} string="Super Type"/>
				<IsPresentP value={object.cards[0].types} string="Types"/>
				<IsPresentP value={object.cards[0].subtypes} string="Sub Types"/>
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
				<IsPresentP value={object.cards[0].rarity} string="Rarity"/>
				<IsPresentP value={object.cards[0].set} string="Set"/>
				<IsPresentP value={object.cards[0].artist} string="Artist"/>
				<IsPresentP value={object.cards[0].number} string="Number"/>
				<IsPresentP value={object.cards[0].multiverseid} string="Multiverse ID"/>
				<IsPresentP value={object.cards[0].id} string="ID"/>
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
				<IsPresentP value={object.cards[0].originalText} string="Originial Text"/>
				<IsPresentP value={object.cards[0].originalType} string="Originial Type"/>
				{#if object.cards[0].rulings}
				<p>Rulings</p>
					{#each object.cards[0].rulings as ruling,i}
					<p>{ruling.date}</p>
					<p>{ruling.text}</p>
				{/each}
				{/if}
			</div>
			</div>
		  </div>
	  </div>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
{/if}
</center>