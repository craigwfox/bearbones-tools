<script>
	$: hexClr = '#000000';
	$: rgbClr = 'rbg(255, 221, 222)';
	$: hslClr = '0, 0%, 0%';

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
</script>

<fieldset id="colorConverter" aria-labelledby="title-color">
	<legend id="title-color">Color converter</legend>
	<div class="input-group">
		<div class="input">
			<label for="hex">Hex</label>
			<input type="text" id="hex" bind:value={hexClr} minlength="6" maxlength="7" />
		</div>
		<div class="input">
			<label for="rgb">RGB</label>
			<input type="text" id="rgb" bind:value={rgbClr} on:blur={rgbToHex(rgbClr)} />
		</div>
	</div>
</fieldset>
