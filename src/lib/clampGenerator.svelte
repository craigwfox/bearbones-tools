<script>
	export let fontBase;
	export let minWin;
	export let maxWin;

	$: minValue = 16;
	$: maxValue = 24;
</script>

<section id="clampgenerator" aria-labelledby="title-clamp">
	<form on:submit|preventDefault={() => {}}>
		<fieldset>
			<legend id="title-clamp">Generate Clamp</legend>
			<div class="input-group">
				<div class="input">
					<label for="pixelsMin">Min value</label>
					<input type="number" id="pixelsMin" bind:value={minValue} />
				</div>
				<div class="input">
					<label for="pixelsMax">Max Value</label>
					<input type="number" id="pixelsMax" bind:value={maxValue} />
				</div>
				<div class="input">
					<label for="windowMin">Window min</label>
					<input type="text" id="windowMin" disabled value={minWin} />
				</div>
				<div class="input">
					<label for="windowMax">Window max</label>
					<input type="text" id="windowMax" disabled value={maxWin} />
				</div>
			</div>
			<code class="output">clamp(1rem, 1rem + 1vw, 2rem)</code>
		</fieldset>
	</form>
</section>

<style type="scss">
	.output {
		display: flex;
		place-content: center;

		margin-block-start: var(--sp-sm);
		padding: var(--sp-sm);

		background: hsl(var(--clr-bg-alt));
		border-radius: var(--rad-2);

		color: hsl(var(--clr-alt-2));
	}

	.input-group {
		grid-template-columns: repeat(auto-fit, minmax(10rem, 1fr));
	}
</style>
