<script>
	import { helpers } from '$lib/helpers';
	export let fontBase;

	$: pixVal = 16;
	$: remVal = 1;

	function remUpdate(val) {
		remVal = parseFloat(helpers.pixToRem(fontBase, val).toFixed(3));
	}

	function pixelUpdate(val) {
		pixVal = parseFloat(helpers.remToPix(fontBase, val).toFixed(3));
	}
</script>

<section id="pxtorem" aria-labelledby="title-pxtorem">
	<fieldset>
		<legend id="title-pxtorem">Convert Pixels to Rems</legend>
		<div>
			<div class="input-group">
				<div class="input">
					<label for="pixels">Pixels</label>
					<input
						type="number"
						id="pixels"
						bind:value={pixVal}
						on:change={(e) => {
							remUpdate(e.target.value);
						}}
						on:keyup={(e) => {
							remUpdate(e.target.value);
						}}
					/>
				</div>
				<div class="input">to</div>
				<div class="input">
					<label for="rems">Rems</label>
					<input
						type="text"
						id="rems"
						bind:value={remVal}
						on:change={(e) => {
							pixelUpdate(e.target.value);
						}}
						on:keyup={(e) => {
							pixelUpdate(e.target.value);
						}}
					/>
				</div>
			</div>
			<div class="exmaple" style="font-size: {pixVal}px">
				<p>Example of text size</p>
			</div>
		</div>
	</fieldset>
</section>

<style type="scss">
	fieldset {
		display: flex;
	}
	fieldset > div {
		display: grid;
		align-content: start;
		justify-content: center;
		grid-template-rows: auto 1fr;
	}

	.input-group {
		grid-template-columns: 1fr auto 1fr;
	}

	.exmaple {
		display: grid;
		place-content: center;
	}

	p {
		margin: 2rem 0 1.7rem;

		font-size: 1em;
	}
</style>
