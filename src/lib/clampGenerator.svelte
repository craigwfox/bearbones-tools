<script>
	import { helpers } from '$lib/helpers';

	export let fontBase;
	export let minWin;
	export let maxWin;

	$: minValue = 16;
	$: maxValue = 24;
	$: clampValue = setTimeout(() => generateClamp());

	$: generateClamp = function () {
		const variablePart = (maxValue - minValue) / (maxWin - minWin);
		const constant = parseFloat(((maxValue - maxWin * variablePart) / 16).toFixed(3));

		clampValue = `clamp(
				${parseFloat(helpers.pixToRem(fontBase, minValue).toFixed(3))}rem,
				${constant}rem + ${parseFloat((100 * variablePart).toFixed(2))}vw,
				${parseFloat(helpers.pixToRem(fontBase, maxValue).toFixed(3))}rem)`;
	};
</script>

<section id="clampgenerator" aria-labelledby="title-clamp">
	<fieldset>
		<legend id="title-clamp">Generate Clamp</legend>
		<div class="input-group">
			<div class="input">
				<label for="pixelsMin">Min <small>(px)</small></label>
				<input
					type="number"
					id="pixelsMin"
					bind:value={minValue}
					on:keyup={() => generateClamp()}
				/>
			</div>
			<div class="input">
				<label for="pixelsMax">Max <small>(px)</small></label>
				<input
					type="number"
					id="pixelsMax"
					bind:value={maxValue}
					on:keyup={() => generateClamp()}
				/>
			</div>
		</div>
		<code class="output">{clampValue}</code>
	</fieldset>
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
		font-size: var(--fs-sm);
	}

	.input-group {
		grid-template-columns: repeat(auto-fit, minmax(10rem, 1fr));
	}
</style>
