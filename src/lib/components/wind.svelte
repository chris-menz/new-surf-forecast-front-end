<script>
    import { _16point } from '$lib/utils/_16point'
	import IconArrowDownCircleOutline from '~icons/mdi/arrow-down-circle-outline'
	
	export let weather;
</script>

<main>
    <div class="header">Wind</div>
    <div class="wind">{weather.wind.speed.toFixed(0)} {+weather.wind.speed.toFixed(0) == 1 ? "kt" : "kts"}
	{#if weather.wind.gust}
		<br>{weather.wind.gust.toFixed(0)} {+weather.wind.gust.toFixed(0) == 1 ? "kt" : "kts"} Gusts
	{/if}<br>{_16point(weather.wind.deg)} {weather.wind.deg}°</div>
	<IconArrowDownCircleOutline style="font-size: 2.5em; transform: rotate({weather.wind.deg}deg)" class="direction-arrow"/>
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
		padding-top: 0.2em;
		font-family: Helvetica, sans-serif;
		font-weight:lighter;
	}

</style>