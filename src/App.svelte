<script>
	let countries = [
		{id: 0, name: "United States"},
		{id: 1, name: "Canada"},
	];

	let us_products = [
		{id: 0, name: "Glue"},
		{id: 1, name: "Tape"},
	];
	let ca_products = [
		{id: 0, name: "Maple Syrup"},
		{id: 1, name: "Lumber"},
	];

	let time_map = new Map([
		["0-0", 33],
		["1-0", 44],
		["0-1", 55],
		["1-1", 66],
	]);

	let selected = {
		country: 0,
		product: 0,
	};

$: time = time_map.get(selected.country + "-" + selected.product);

</script>

<main>
	<div>
		<select bind:value={selected.country}>
			{#each countries as country}
			<option value={country.id}>
				{country.name}
			</option>
			{/each}
		</select>
		<p>Selected Country: {selected.country}</p>
	</div>
	{#if selected.country === 0 }
	<div>
		<select bind:value={selected.product}>
			{#each us_products as product}
			<option value={product.id}>
				{product.name}
			</option>
			{/each}
		</select>
		<p>{selected.product}</p>
	</div>
	{:else }
	<div>
		<select bind:value={selected.product}>
			{#each ca_products as product}
			<option value={product.id}>
				{product.name}
			</option>
			{/each}
		</select>
		<p>{selected.product}</p>
	</div>
	{/if}
	<div>
		<p>Time: {time}</p>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
