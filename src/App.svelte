<script>
	import * as Pancake from '@sveltejs/pancake';
	import Select from './Select.svelte'

const us_glue_points = [
	{ year: 2019, value: 5000 },
	{ year: 2018, value: 6000 },
	{ year: 2017, value: 2000 },
	{ year: 2016, value: 8000 },
];
const us_tape_points = [
	{ year: 2019, value: 2000 },
	{ year: 2018, value: 3000 },
	{ year: 2017, value: 1000 },
	{ year: 2016, value: 4000 },
];
const ca_maple_points = [
	{ year: 2019, value: 9000 },
	{ year: 2018, value: 3000 },
	{ year: 2017, value: 8000 },
	{ year: 2016, value: 2000 },
];
const ca_lumber_points = [
	{ year: 2019, value: 7000 },
	{ year: 2018, value: 1000 },
	{ year: 2017, value: 8000 },
	{ year: 2016, value: 1000 },
];

	let countries = [
		{id: "0", name: "United States"},
		{id: "1", name: "Canada"},
	];

	let us_products = [
		{id: "0", name: "Glue"},
		{id: "1", name: "Tape"},
	];
	let ca_products = [
		{id: "2", name: "Maple Syrup"},
		{id: "3", name: "Lumber"},
	];

	let time_map = new Map([
		["0-0", 33],
		["0-1", 44],
		["1-2", 55],
		["1-3", 66],
	]);

	// NOTE big note, `select` always returns a string. So if I want to use a number, `===` won't work.
	// Maybe should just keep it as all strings.
	let selected_country = "0";
	let selected_product_us = "0";
	let selected_product_ca = "2";


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

	// for chart
	let miny = +Infinity;
	let maxy = -Infinity;
</script>

<main>
	<div>
		<Select label="Country:" options={countries} value={selected_country} on_change="{ev => update_selected_country(ev.target.value)}">
		</Select>
		<p>Selected Country: {selected_country}</p>
	</div>
	{#if selected_country === "0" }
	<div>
		<Select label="Product:" options={us_products} value={selected_product_us} on_change="{ev => update_selected_product_us(ev.target.value)}">
		</Select>
		<p>Selected Product: {selected_product_us}</p>
	</div>
	{:else if selected_country === "1" }
	<div>
		<Select label="Product:" options={ca_products} value={selected_product_ca} on_change="{ev => update_selected_product_ca(ev.target.value)}">
		</Select>
		<p>Selected Product: {selected_product_ca}</p>
	</div>
	{/if}

	{#if selected_country === "0" }
	<div>
		<p>US product Time: {us_time}</p>
	</div>
	{:else if selected_country === "1" }
	<div>
		<p>CA product Time: {ca_time}</p>
	</div>
	{/if}
</main>

<section class="hero">
	<div class="chart">
		<Pancake.Chart x1={2016} x2={2019} y1={0} y2={10000}>
			<Pancake.Grid horizontal count={10} let:value let:last>
				<div class="grid-line horizontal"><span>{value} {last ? 'dollars' : ''}</span></div>
			</Pancake.Grid>
			<Pancake.Grid vertical count={4} let:value>
				<div class="grid-line vertical"></div>
				<span class="year-label">{value}</span>
			</Pancake.Grid>

			<Pancake.Svg>
				<Pancake.SvgLine data={us_tape_points} x="{d => d.year}" y="{d => d.value}" let:d>
					<path class="line" {d}/>
				</Pancake.SvgLine>
			</Pancake.Svg>
		</Pancake.Chart>
	</div>
</section>

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

	@media (min-width: 800px) {
		main {
			max-width: none;
		}
		.chart {
			height: 600px
		}
	}

	.hero {
		margin: 0 auto 4em auto;
		max-width: 80em;
	}

		.chart {
		height: 450px;
		padding: 3em 0 2em 2em;
		margin: 0 0 36px 0;
		max-width: 50em;
		margin: 0 auto;
	}
	.grid-line {
		position: relative;
		display: block;
	}
	.grid-line.horizontal {
		width: calc(100% + 2em);
		left: -2em;
		border-bottom: 1px dashed #ccc;
	}
	.grid-line.vertical {
		height: 100%;
		border-left: 1px dashed #ccc;
	}
	.grid-line span {
		position: absolute;
		left: 0;
		bottom: 2px;
		line-height: 1;
		font-family: sans-serif;
		font-size: 14px;
		color: #999;
	}
	.year-label {
		position: absolute;
		width: 4em;
		left: -2em;
		bottom: -30px;
		font-family: sans-serif;
		font-size: 14px;
		color: #999;
		text-align: center;
	}
		path.line {
		stroke: #ff3e00;
		opacity: 0.5;
		stroke-linejoin: round;
		stroke-linecap: round;
		stroke-width: 2px;
		fill: none;
	}
</style>
