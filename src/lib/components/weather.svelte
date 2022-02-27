<script>
	export let weather;	
	export let conditions;
	let url = `http://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`
</script>

<main>
    <div class="card">
		<div class="header">Weather</div>
		<div class="weather-container">
			<div class="weather">
				<div>Water: {conditions.water_temperature}°f</div>
				<div>Air: {weather.main.temp.toFixed(0)}°f</div>
				<div>{weather.weather[0].main}</div>
			</div>
			
			<!-- <img src={url} alt="weather"> -->
		</div>
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
	}

	.header {
		font-size: 2em;
		font-family: Verdana, sans-serif;
		text-decoration: underline;
	}

	.weather {
		padding: 0.3em 0;
		font-size: 1.2em;
		line-height: 1.2em;
		font-family: Helvetica, sans-serif;
		font-weight:lighter;
	}

	/* img {
		margin-top: -1.3em;
		margin-left: -1em;
	} */
</style>