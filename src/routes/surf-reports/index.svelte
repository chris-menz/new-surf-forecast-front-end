<script lang="ts">
    import Nav from "$lib/components/nav.svelte";
	import Menu from "$lib/components/menu.svelte"
	import ConditionsDashboard from "$lib/components/conditionsDashboard.svelte";
	import SavedSpotsDashboard from "$lib/components/savedSpotsDashboard.svelte";
	import { fly } from "svelte/transition";
	import { onMount } from "svelte";
	import { user } from "$lib/stores/userStore"

	let mySpotsViewActive;
	let searchViewActive;

	const toggleMySpotsView = () => {
		mySpotsViewActive = true
		searchViewActive = false
	}

	const toggleSearchView = () => {
		mySpotsViewActive = false
		searchViewActive = true
	}

    let region: string;
    let surf_break_name: string;

	let hasSearched: boolean

	onMount(async () => {
		hasSearched = false;

        if($user){
			toggleMySpotsView()
        }
        else {
			toggleSearchView()
        }
	})
</script>

<main class="small-screen-view">
	<Nav />
	{#if !hasSearched}
		<div class="tabs" in:fly="{{ delay: 500, duration: 250 }}">
			<div class="tab" style="background: {mySpotsViewActive ? "linear-gradient(to right bottom, #6a37c2, #49329e)" : "none"}" on:click={() => toggleMySpotsView()}>My Spots</div>
			<div class="tab" style="background: {searchViewActive ? "linear-gradient(to right bottom, #6a37c2, #49329e)" : "none"}" on:click={() => toggleSearchView()}>Search</div>
		</div>
		{#if mySpotsViewActive}
		<div class="spots-dashboard-container">
			<SavedSpotsDashboard on:fullReportRequest={e => {region = e.detail.region; surf_break_name = e.detail.surf_break; hasSearched = true;}}/>
		</div>
		{/if}
		{#if searchViewActive}
		<div class="menu-container">
			<Menu on:breakChange={e => {region = e.detail.region; surf_break_name = e.detail.surf_break; hasSearched = true;}}/>
		</div>
		{/if}
	{/if}
	
	{#if hasSearched}
		<ConditionsDashboard {region} {surf_break_name}/>
	{/if}
</main>

<main class="large-screen-view">
    <Nav />
	{#if !hasSearched}
		<div class="dashboard-container" in:fly="{{ delay: 500, duration: 250 }}">
			<div class="menu-container">
				<Menu on:breakChange={e => {region = e.detail.region; surf_break_name = e.detail.surf_break; hasSearched = true;}}/>
			</div>
			<div class="spots-dashboard-container">
				<SavedSpotsDashboard on:fullReportRequest={e => {region = e.detail.region; surf_break_name = e.detail.surf_break; hasSearched = true;}}/>
			</div>
		</div>
	{/if}
    

	{#if hasSearched}
		<ConditionsDashboard {region} {surf_break_name}/>
	{/if}
</main>

<style>
	
	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}

	:global(body) {
        background-color: #161616;
        transition: background-color 0.3s
    }

	.small-screen-view {
		display: none
	}

	

	.tabs {
		display: none;
		top: 3.90em;
		left: 0%;
		position: fixed;
		background-color: #2b2b2b;
		width: 100vw;
		height: 50px;
		cursor: pointer;
	}

	.tab {
		color: white;
		width: 50%;
		display: grid;
		place-content: center;
		text-transform: uppercase;
		font-family: Verdana, Geneva, Tahoma, sans-serif;
	}

	.menu-container {
		display: grid;
		place-content: center;
		height: 100vh;
	}

	.dashboard-container {
		display: flex;
		flex-direction: row;
		justify-content: space-evenly;
		align-items: flex-start;
		height: 100vh;
	}

	.spots-dashboard-container {
		margin-top: 5em;
	}

	button {
        position: relative;
        background: linear-gradient(to right bottom, #6a37c2, #49329e);
        text-align: center;
        font-family: Verdana;
        font-size: 1.1em;
        color: rgb(240, 234, 234);
        max-width: 80%;
        padding: 0.5em 1em;
        border-radius: 5px;
        margin-top: 3.5em;
        border: none;
        cursor: pointer;
        box-shadow: rgba(0, 0, 0, 0.3) 0px 4px 12px;
        transition-duration: 300ms;
        z-index: 1;
    }

    button::before{
		position: absolute;
		content: "";
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		border-radius: 5px;
		background: linear-gradient(to right bottom, rgb(59, 31, 110),rgb(57, 39, 122)0);
		transition: opacity 0.3s;
		z-index: -1;
		opacity: 0;
	}

    button:hover::before {
		opacity: 1;
	}

    button:hover {
        color: rgb(182, 182, 182);
    }
	@media (max-width: 950px) {
		.large-screen-view {
			display: none;
		}

		.small-screen-view {
			display:inherit; 
		}

		.tabs {
			display: flex;
		}
		
	}

	@media (max-width: 700px) {
		.tabs {
			top: 3.3em;
		}
	}

</style>