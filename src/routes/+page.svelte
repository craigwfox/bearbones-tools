<script>
	import ClampGenerator from '../lib/clampGenerator.svelte';
	import ColorConverter from '../lib/colorConverter.svelte';
	import PxToRem from '../lib/pxToRem.svelte';

	$: fsBase = 16;
	$: minWidth = 375;
	$: maxWidth = 1200;
</script>

<form on:submit|preventDefault={() => {}}>
	<fieldset class="controls">
		<legend>Default values (in pixels)</legend>
		<div class="input-group">
			<div class="input">
				<label for="sizeBase">Base size</label>
				<input type="number" id="sizeBase" bind:value={fsBase} />
			</div>
			<div class="input">
				<label for="minWidth">Min window width</label>
				<input type="number" id="minWidth" bind:value={minWidth} />
			</div>
			<div class="input">
				<label for="maxWidth">Max window width</label>
				<input type="number" id="maxWidth" bind:value={maxWidth} />
			</div>
		</div>
	</fieldset>

	<div class="tools">
		<PxToRem fontBase={fsBase} />
		<ColorConverter />
		<ClampGenerator fontBase={fsBase} minWin={minWidth} maxWin={maxWidth} />
	</div>
</form>

<style type="scss">
	fieldset {
		height: 100%;
		border: 0.3rem solid hsl(var(--clr-alt-1));
	}

	legend {
		margin: 0;
		padding-inline: 0.5rem;

		color: hsl(var(--clr-alt-2));
		font-weight: 700;
	}

	.input-group {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(13rem, 1fr));
		align-items: end;
		gap: 0.5rem var(--sp-sm);
	}

	.input input {
		width: 100%;

		display: block;

		padding-inline: 0.5rem;

		border: 0.2rem solid hsl(var(--clr-bg-alt));

		color: hsl(var(--clr-bg-alt));

		&:invalid {
			border-color: hsl(var(--clr-main));
		}

		&:disabled {
			background: hsl(0 0% 80%);

			color: hsl(var(--clr-bg-alt) / 0.7);
		}
	}
	.input label {
		display: block;

		color: hsl(var(--clr-alt-1));
		font-weight: 700;
	}

	.controls {
		margin-block-end: var(--sp-lg);
	}

	.tools {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
		gap: var(--sp-lg) var(--sp-lg);
	}
</style>
