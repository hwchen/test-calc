<script>
	import Select from './Select.svelte'
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

	// Just using two-way binding for selects. Should be fine for selects?
	//Will it cause problems on larger projects?
	let selected_country;
	let selected_product_us;
	let selected_product_ca;


	// have to use string as key; svelte cannot see into arrays.
	$: us_time = time_map.get(selected_country + "-" + selected_product_us);
	$: ca_time = time_map.get(selected_country + "-" + selected_product_ca);

</script>

<main>
	<div>
		<Select label="Country:" options={countries} bind:value={selected_country}>
		</Select>
		<p>Selected Country: {selected_country}</p>
	</div>
	{#if selected_country === 0 }
	<div>
		<Select label="Product:" options={us_products} bind:value={selected_product_us}>
		</Select>
		<p>Selected Product: {selected_product_us}</p>
	</div>
	{:else }
	<div>
		<Select label="Product:" options={ca_products} bind:value={selected_product_ca}>
		</Select>
		<p>Selected Product: {selected_product_ca}</p>
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
