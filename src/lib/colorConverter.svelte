<script>
	import { onMount } from 'svelte';

	// #ff5757
	// rgb(255, 87, 87)
	// hsl(0, 100%, 67%)
	$: hexClr = '#FF5757';
	// $: rgbClr = 'rbg(223, 221, 180)';
	$: rgbClr = 'rbg(0, 0, 0)';
	$: hslClr = 'hsl(0, 0%, 0%)';

	const hexTable = {
		'0': '0',
		'1': '1',
		'2': '2',
		'3': '3',
		'4': '4',
		'5': '5',
		'6': '6',
		'7': '7',
		'8': '8',
		'9': '9',
		'10': 'A',
		'11': 'B',
		'12': 'C',
		'13': 'D',
		'14': 'E',
		'15': 'F'
	};

	function rgbToHex(val) {
		const valArry = [...val.match(/(\d*)/g, '')].filter((x) => x.length > 0);
		let hexVal = '#';

		valArry.forEach((num) => {
			const num1 = Math.trunc(num / 16);
			const num2 = (num / 16 - num1) * 16;
			hexVal += `${hexTable[num1]}${hexTable[num2]}`;
		});

		hexClr = hexVal;
	}

	function scanHexTable(val) {
		return Object.keys(hexTable).find((key) => hexTable[key].toLowerCase() === val.toLowerCase());
	}

	function hexToRgb(val) {
		const valClean = val.replace(/[\#]/g, '');
		const valArry = valClean.match(/(\w{2})/g);
		let rbgVal = 'rgb(';

		if (valClean.length != 6) return false;
		valArry.forEach((num, key, arr) => {
			const num1 = scanHexTable(num[0]) * 16;
			const num2 = (scanHexTable(num[1]) * 16) / 16;

			rbgVal += num1 + num2;
			!Object.is(arr.length - 1, key) ? (rbgVal += ', ') : (rbgVal += ')');
		});

		rgbClr = rbgVal;
	}

	onMount(async () => {
		// rgbToHex(rgbClr);
		hexToRgb(hexClr);
	});
</script>

<fieldset id="colorConverter" aria-labelledby="title-color">
	<legend id="title-color">Color converter</legend>
	<div class="input-group">
		<div class="input">
			<label for="hex">Hex <span class="clr-sample" style="--bg-val: {hexClr};" /></label>
			<input
				type="text"
				id="hex"
				minlength="6"
				maxlength="7"
				bind:value={hexClr}
				on:keyup={hexToRgb(hexClr)}
			/>
		</div>
		<div class="input">
			<label for="rgb">RGB <span class="clr-sample" style="--bg-val: {rgbClr};" /></label>
			<input type="text" id="rgb" bind:value={rgbClr} on:keyup={rgbToHex(rgbClr)} />
		</div>
		<div class="input">
			<label for="hsl">HSL <span class="clr-sample" style="--bg-val: {hslClr};" /></label>
			<input type="text" id="hsl" bind:value={hslClr} />
		</div>
	</div>
</fieldset>

<style type="scss">
	.input {
		label {
			display: flex;
			align-items: center;

			gap: 1rem;

			span {
				height: 1em;

				flex: 1 0 5rem;

				margin-inline-end: 0.2rem;

				background: var(--bg-val);
				border: 0.1rem solid white;

				transition: all 0.2s ease-in-out;
			}
		}
	}
</style>
