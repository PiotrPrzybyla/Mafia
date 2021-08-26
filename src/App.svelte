<script>
	import PlayerName from "./PlayerName.svelte";
	import RoleList from "./RoleList.svelte";
	let playersAmount = 1;
	let players = [""];
	let finalPlayers;
	let numberIsChosen = false;
function refreshPlayer(){
	players.length = playersAmount
	players = players;

}

function submitPlayers(){
	
		
	finalPlayers = players;
	console.log(finalPlayers)
	numberIsChosen = true

		

}
	
</script>

<h1>Ktoś dzisiaj zginie!</h1>
{#if numberIsChosen}
<RoleList finalPlayersAmount = {finalPlayers.length} bind:finalPlayers = {finalPlayers}/>

{:else}
<form on:submit={submitPlayers}>
<label for="playerCounter"> Podaj liczbę graczy</label>
<input type="number" name = "playerCounter" bind:value={playersAmount} min="1" on:change={refreshPlayer}>
{#each players as player, i}
	<PlayerName playerNumber={i} bind:playerName={player} />
{/each}
<button type="submit">Dalej</button>
</form>
{/if}





<style>
	

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		
	}
</style>