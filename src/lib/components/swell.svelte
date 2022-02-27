<script>
	import { _16point } from '$lib/utils/_16point'
	import SvelteTooltip from 'svelte-tooltip';
	
	const tooltip = "Swell is a measure of ocean energy. It can give us a rough estimate of how big the waves are"
	export let conditions;
</script>

<main>
	<div class="card">
		<div class="header-container">
			<div class="header">Swell</div>
			<div class="tooltip">
				<SvelteTooltip tip={tooltip} color="#111111" top>?</SvelteTooltip>
			</div>
			
		</div>
		

		<div class="swell">{conditions.swell_height} ft. @ {conditions.swell_period}s<br>{_16point(+conditions.swell_direction)} {conditions.swell_direction}°</div>
		<!-- <div class="direction-arrow">
			<Fa icon={faArrowAltCircleDown} size="2.5x" style="transform: rotate({conditions.swell_direction}deg);"/>
		</div> -->
		{#if +conditions.wind_wave_height > 1  && +conditions.wind_wave_height > +conditions.secondary_swell_height}
			<div class="swell">{conditions.wind_wave_height} ft. @ {conditions.wind_wave_period}s<br>{_16point(+conditions.wind_wave_direction)} {conditions.wind_wave_direction}°</div>
			<!-- <div class="direction-arrow">
				<Fa icon={faArrowAltCircleDown} size="2.5x" style="transform: rotate({conditions.wind_wave_direction}deg);"/>
			</div> -->
		{/if}

		{#if +conditions.secondary_swell_height > 1 && +conditions.wind_wave_height < +conditions.secondary_swell_height}
			<div class="swell">{conditions.secondary_swell_height} ft. @ {conditions.secondary_swell_period}s<br>{_16point(+conditions.secondary_swell_direction)} {conditions.secondary_swell_direction}°</div>
			<!-- <div class="direction-arrow">
				<Fa icon={faArrowAltCircleDown} size="2.5x" style="transform: rotate({conditions.secondary_swell_direction}deg);"/>
			</div> -->
		{/if}
		
	</div>
</main>

<style>

	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}

	.card {
		max-width: 250px;
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.header-container {
		display: flex;
		flex-direction: row;
		align-items: center;
	}

	.header {
		font-size: 2em;
		font-family: Verdana, sans-serif;
		text-decoration: underline;
	}

	.swell {
		font-size: 1.2em;
		padding: 0.3em;
		font-family: Helvetica, sans-serif;
		font-weight:lighter;
	}

	.tooltip {
		font-size: 14px;
		margin: 2px;
		font-family: Helvetica, sans-serif;
		font-weight: lighter;
		color: rgb(151, 151, 151);
		width: 2px;
	}

	.tooltip:hover {
		color: white;
		cursor: pointer;
	}
</style>