<script>
	export let label = "Default label";
	export let options = [];
	export let value = undefined;
	export let on_change = undefined;
</script>

<label>
	{label}
	<select on:change={on_change}>
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
