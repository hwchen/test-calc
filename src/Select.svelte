<script>
	export let label = "Default label";
	export let options = [];

	// undefined prevents warning about Component created with expected prop.
	// Not sure the best way to handle this; right now I expect to bind to value prop, what happens when I don't?
	export let value = undefined;
</script>

<label>
	{label}
	<select bind:value={value}>
		{#if options.length}
			{#each options as option}
				<option value={option.id} selected={option.id === value ? true : null}>
					{option.name}
				</option>
			{/each}
		{:else}
			<option>Missing `options` array</option>
		{/if}
	</select>
</label>
