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
		{id: 2, name: "Maple Syrup"},
		{id: 3, name: "Lumber"},
	];

	let time_map = new Map([
		["0-0", 33],
		["0-1", 44],
		["1-2", 55],
		["1-3", 66],
	]);

	let selected_country;
	let selected_product_us;
	let selected_product_ca;


$: us_time = time_map.get(selected_country + "-" + selected_product_us);
$: ca_time = time_map.get(selected_country + "-" + selected_product_ca);

</script>

<main>
	<div>
		<select bind:value={selected_country}>
			{#each countries as country}
			<option value={country.id}>
				{country.name}
			</option>
			{/each}
		</select>
		<p>Selected Country: {selected_country}</p>
	</div>
	{#if selected_country === 0 }
	<div>
		<select bind:value={selected_product_us}>
			{#each us_products as product}
			<option value={product.id}>
				{product.name}
			</option>
			{/each}
		</select>
		<p>{selected_product_us}</p>
	</div>
	{:else }
	<div>
		<select bind:value={selected_product_ca}>
			{#each ca_products as product}
			<option value={product.id}>
				{product.name}
			</option>
			{/each}
		</select>
		<p>{selected_product_ca}</p>
	</div>
	{/if}

	{#if selected_country === 0 }
	<div>
		<p>Time: {us_time}</p>
	</div>
	{:else }
	<div>
		<p>Time: {ca_time}</p>
	</div>
	{/if}
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
