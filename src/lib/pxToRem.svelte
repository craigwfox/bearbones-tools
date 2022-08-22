<script>
	export let baseSize;

	$: pixVal = 16;
	$: remVal = 1;

	function convertPixToRem(val) {
		remVal = val / baseSize;
	}

	function convertRemToPix(val) {
		pixVal = val * baseSize;
	}
</script>

<section id="pxtorem" aria-labelledby="title-pxtorem">
	<form on:submit|preventDefault={() => {}}>
		<fieldset>
			<legend id="title-pxtorem">Convert Pixels to Rems</legend>
			<div class="input-group">
				<div class="input">
					<label for="pixels">Pixels</label>
					<input
						type="number"
						id="pixels"
						bind:value={pixVal}
						on:keyup={(e) => {
							convertPixToRem(e.target.value);
						}}
					/>
				</div>
				<div class="input">to</div>
				<div class="input">
					<label for="rems">Rems</label>
					<input
						type="number"
						id="rems"
						bind:value={remVal}
						on:keyup={(e) => {
							convertRemToPix(e.target.value);
						}}
					/>
				</div>
			</div>
		</fieldset>
	</form>
</section>

<style type="scss">
	fieldset {
		max-width: 25rem;
	}

	.input-group {
		grid-template-columns: 1fr auto 1fr;
	}
</style>
