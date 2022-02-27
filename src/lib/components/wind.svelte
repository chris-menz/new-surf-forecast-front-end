<script>
    import { _16point } from '$lib/utils/_16point'
	import Fa from 'svelte-fa/src/fa.svelte'
    import { faArrowAltCircleDown } from '@fortawesome/free-regular-svg-icons'
	
	export let weather;
</script>

<main>
    <div class="header">Wind</div>
    <div class="wind">{weather.wind.speed.toFixed(0)} {+weather.wind.speed.toFixed(0) == 1 ? "kt" : "kts"}
	{#if weather.wind.gust}
		<br>{weather.wind.gust.toFixed(0)} {+weather.wind.gust.toFixed(0) == 1 ? "kt" : "kts"} Gusts
	{/if}<br>{_16point(weather.wind.deg)} {weather.wind.deg}°</div>
	<div class="direction-arrow">
		<Fa icon={faArrowAltCircleDown} size="2.5x" style="transform: rotate({weather.wind.deg}deg);"/>
	</div>
</main>

<style>
	:root{
		--deg: 0deg;
	}
	
	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}

	.header {
		font-size: 2em;
		font-family: Verdana, sans-serif;
		text-decoration: underline;
	}

	.wind {
		font-size: 1.3em;
		padding: 0.2em;
		font-family: Helvetica, sans-serif;
		font-weight:lighter;
	}

</style>