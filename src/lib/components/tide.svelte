<script>
	import { onMount } from 'svelte'
	import { convert24HrToAmPm } from '$lib/utils/dateTimeUtils'
	
	export let tideExtremes;
	export let tideHeight;
	export let localDate;
	let curr_tide_data = tideExtremes.get(localDate.toString().split("T")[0]);;

	let tide_string_array = [];
	
	onMount(async () => {
		for(let i = 0; i < curr_tide_data.length; ++i){
			const tide = curr_tide_data[i]
			const time = convert24HrToAmPm(tide.date.substring(11, 16))
			tide_string_array[i] = `${tide.type}: ${Math.round(tide.height * 3.281 * 10) / 10} ft, ${time}`;
		}
	})

	
</script>

<main>
    <div class="header">Tide</div>
	<div class="tides">
		<div class="tide-height">{tideHeight.height} ft, {tideHeight.state}</div>
		{#each tide_string_array as tide}
			<div class="tide">{tide}</div>
		{/each}
	</div>
	
</main>

<style>
	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}

	.header {
		font-family: Verdana, sans-serif;
		font-size: 2em;
		text-decoration: underline;
	}

	.tides {
		line-height: 1.3em;
		font-size: 1em;
		padding: 0.4em 0;
		font-family: Helvetica, sans-serif;
		font-weight:lighter;
	}

	.tide-height {
		font-size: 1.3em;
		padding-bottom: 00.1em;
	}

	.tide {
		padding: 0.1em;
		font-size: 1em;
	}

	@media(max-width: 500px) {
		.tide {
			font-size: 00.9em;
		}
	}
</style>