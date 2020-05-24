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

	// NOTE big note, `select` always returns a string. So if I want to use a number, `===` won't work.
	// Maybe should just keep it as all strings.
	let selected_country = 0;
	let selected_product_us = 0;
	let selected_product_ca = 2;


	// have to use string as key; svelte cannot see into arrays.
	// this should automatically update when selected is manually updated
	$: us_time = time_map.get(selected_country + "-" + selected_product_us);
	$: ca_time = time_map.get(selected_country + "-" + selected_product_ca);

	function update_selected_country(value) {
		selected_country = value;
	}
	function update_selected_product_us(value) {
		selected_product_us = value;
	}
	function update_selected_product_ca(value) {
		selected_product_ca = value;
	}
</script>

<main>
	<div>
		<Select label="Country:" options={countries} value={selected_country} on_change="{ev => update_selected_country(ev.target.value)}">
		</Select>
		<p>Selected Country: {selected_country}</p>
	</div>
	{#if selected_country == 0 }
	<div>
		<Select label="Product:" options={us_products} value={selected_product_us} on_change="{ev => update_selected_product_us(ev.target.value)}">
		</Select>
		<p>Selected Product: {selected_product_us}</p>
	</div>
	{:else if selected_country == 1}
	<div>
		<Select label="Product:" options={ca_products} value={selected_product_ca} on_change="{ev => update_selected_product_ca(ev.target.value)}">
		</Select>
		<p>Selected Product: {selected_product_ca}</p>
	</div>
	{/if}

	{#if selected_country == 0 }
	<div>
		<p>US product Time: {us_time}</p>
	</div>
	{:else if selected_country == 2}
	<div>
		<p>CA product Time: {ca_time}</p>
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
