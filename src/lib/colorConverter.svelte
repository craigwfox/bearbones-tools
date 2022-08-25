<script>
	import { onMount } from 'svelte';

	// #ff5757
	// rgb(255, 87, 87)
	// hsl(0, 100%, 67%)
	$: hexClr = '#FF5757';
	$: rgbClr = 'rgb(255, 87, 87)';
	$: hslClr = 'hsl(0, 100%, 67%)';

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

	// From https://css-tricks.com/converting-color-spaces-in-javascript/
	function rgbToHsl(val) {
		const valArry = [...val.match(/(\d*)/g, '')].filter((x) => x.length > 0);

		let r = parseInt(valArry[0]);
		let g = parseInt(valArry[1]);
		let b = parseInt(valArry[2]);

		// Make r, g, and b fractions of 1
		r /= 255;
		g /= 255;
		b /= 255;

		// Find greatest and smallest channel values
		let cmin = Math.min(r, g, b),
			cmax = Math.max(r, g, b),
			delta = cmax - cmin,
			h = 0,
			s = 0,
			l = 0;

		// Calculate hue
		// No difference
		if (delta == 0) h = 0;
		// Red is max
		else if (cmax == r) h = ((g - b) / delta) % 6;
		// Green is max
		else if (cmax == g) h = (b - r) / delta + 2;
		// Blue is max
		else h = (r - g) / delta + 4;

		h = Math.round(h * 60);

		// Make negative hues positive behind 360°
		if (h < 0) h += 360;

		// Calculate lightness
		l = (cmax + cmin) / 2;

		// Calculate saturation
		s = delta == 0 ? 0 : delta / (1 - Math.abs(2 * l - 1));

		// Multiply l and s by 100
		s = +(s * 100).toFixed(1);
		l = +(l * 100).toFixed(1);

		hslClr = 'hsl(' + h + ',' + s + '%,' + l + '%)';
	}

	// Also from https://css-tricks.com/converting-color-spaces-in-javascript/
	function hslToRgb(val) {
		const valArry = [...val.match(/(\d*)/g, '')].filter((x) => x.length > 0);

		let h = parseInt(valArry[0]);
		let s = parseInt(valArry[1]);
		let l = parseInt(valArry[2]);

		// Must be fractions of 1
		s /= 100;
		l /= 100;

		let c = (1 - Math.abs(2 * l - 1)) * s,
			x = c * (1 - Math.abs(((h / 60) % 2) - 1)),
			m = l - c / 2,
			r = 0,
			g = 0,
			b = 0;

		if (0 <= h && h < 60) {
			r = c;
			g = x;
			b = 0;
		} else if (60 <= h && h < 120) {
			r = x;
			g = c;
			b = 0;
		} else if (120 <= h && h < 180) {
			r = 0;
			g = c;
			b = x;
		} else if (180 <= h && h < 240) {
			r = 0;
			g = x;
			b = c;
		} else if (240 <= h && h < 300) {
			r = x;
			g = 0;
			b = c;
		} else if (300 <= h && h < 360) {
			r = c;
			g = 0;
			b = x;
		}
		r = Math.round((r + m) * 255);
		g = Math.round((g + m) * 255);
		b = Math.round((b + m) * 255);

		rgbClr = 'rgb(' + r + ',' + g + ',' + b + ')';
	}

	onMount(async () => {
		// rgbToHex(rgbClr);
		// hexToRgb(hexClr);
		// hslToRgb(hslClr);
	});
</script>

<fieldset id="colorConverter" aria-labelledby="title-color">
	<legend id="title-color">Color converter</legend>
	<span class="clr-sample" style="--bg-val: {hexClr};" />
	<div class="input-group">
		<div class="input">
			<label for="hex">Hex</label>
			<input
				type="text"
				id="hex"
				minlength="6"
				maxlength="7"
				bind:value={hexClr}
				on:keyup={(hexToRgb(hexClr), rgbToHsl(rgbClr))}
			/>
		</div>
		<div class="input">
			<label for="rgb">RGB</label>
			<input
				type="text"
				id="rgb"
				bind:value={rgbClr}
				on:keyup={(rgbToHex(rgbClr), rgbToHsl(rgbClr))}
			/>
		</div>
		<div class="input">
			<label for="hsl">HSL</label>
			<input
				type="text"
				id="hsl"
				bind:value={hslClr}
				on:keyup={(hslToRgb(hslClr), rgbToHex(rgbClr))}
			/>
		</div>
	</div>
</fieldset>

<style type="scss">
	.clr-sample {
		width: 100%;
		height: 2rem;

		display: grid;

		margin-block-end: 0.5rem;

		background: var(--bg-val);
		border: 0.1rem solid white;

		transition: all 0.2s ease-in-out;
	}
</style>
