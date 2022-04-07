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
	<p>text</p><IsPresentP value={object.cards[0].text}/>
	<p>power</p><IsPresentP value={object.cards[0].power}/>
	<p>toughness</p><IsPresentP value={object.cards[0].toughness}/>






	<div class="accordion" id="accordionPanelsStayOpenExample">
		<div class="accordion-item">
		  <h2 class="accordion-header" id="panelsStayOpen-headingOne">
			<button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseOne" aria-expanded="true" aria-controls="panelsStayOpen-collapseOne">
			  Mana and colours
			</button>
		  </h2>
		  <div id="panelsStayOpen-collapseOne" class="accordion-collapse collapse" aria-labelledby="panelsStayOpen-headingOne">
			<div class="accordion-body">
				<p>manaCost</p><IsPresentP value={object.cards[0].manaCost}/>
				<p>cmc</p><IsPresentP value={object.cards[0].cmc}/>
				<p>colors</p><IsPresentP value={object.cards[0].colors}/>
				<p>colorIdentity</p><IsPresentP value={object.cards[0].colorIdentity}/>
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
				<p>type</p><IsPresentP value={object.cards[0].type}/>
				<p>supertypes</p><IsPresentP value={object.cards[0].supertypes}/>
				<p>types</p><IsPresentP value={object.cards[0].types}/>
				<p>subtypes</p><IsPresentP value={object.cards[0].subtypes}/>
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
				<p>rarity</p><IsPresentP value={object.cards[0].rarity}/>
				<p>set</p><IsPresentP value={object.cards[0].set}/>
				<p>artist</p><IsPresentP value={object.cards[0].artist}/>
				<p>number</p><IsPresentP value={object.cards[0].number}/>
				<p>multiverseid</p><IsPresentP value={object.cards[0].multiverseid}/>
				<p>id</p><IsPresentP value={object.cards[0].id}/>
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
				<p>rulings</p><IsPresentP value={object.cards[0].rulings}/>
				<p>originalText</p><IsPresentP value={object.cards[0].originalText}/>
				<p>originalType</p><IsPresentP value={object.cards[0].originalType}/>
			
			  </div>
			</div>
		  </div>
	  </div>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
</center>