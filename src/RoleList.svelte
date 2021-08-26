<script>
import { each } from "svelte/internal";
 export let finalPlayersAmount
 export let mafiaAmount = 1;
 export let popeAmount = 0;
 export let amorAmount = 0;
 export let policeAmount = 0;
 export let finalPlayers;
 let actualPlayer = "";
 let actualRole = "";
 let isDrawed = false;
 let isRoleSeen = false;
 const rolesToDraw = [];
 function shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
}
 function drawRoles() {
   
    let normalPlayers = finalPlayersAmount - (mafiaAmount+popeAmount+amorAmount+policeAmount);
    for(let i = 0; i < normalPlayers; i++){
        rolesToDraw.push("Zwykły obywatel");
    }
    for(let i = 0; i < mafiaAmount; i++){
        rolesToDraw.push("Mafia");
    }
    for(let i = 0; i < popeAmount; i++){
        rolesToDraw.push("Papież");
    }
    for(let i = 0; i < amorAmount; i++){
        rolesToDraw.push("Amor");
    }
    for(let i = 0; i < policeAmount; i++){
        rolesToDraw.push("Policja");
    }
    shuffleArray(rolesToDraw);
    console.log(rolesToDraw)
    console.log(finalPlayers)
    isDrawed = true;
    actualPlayer = finalPlayers[0];
    actualRole = rolesToDraw[0];
    
 }
 function showRole(){
   
   
    actualRole = rolesToDraw[0];
    isRoleSeen = !isRoleSeen;
    }
 
 function nextPlayer(){
    if(finalPlayers.length ==0){
        alert("No players")
    }
    else{
    finalPlayers.shift();
    rolesToDraw.shift();
    console.log(finalPlayers)
    actualPlayer = finalPlayers[0];
    isRoleSeen = !isRoleSeen;
    }

 }
 
</script>
{#if isDrawed == false}
<p>Liczba graczy: {finalPlayersAmount}</p>
<form on:submit={drawRoles}>
<label for="mafia">Mafia:</label>
<input  type="number" name="mafia" bind:value={mafiaAmount} min="1" max={finalPlayersAmount -(popeAmount+amorAmount+policeAmount) }>

<label for="pope">Papież:</label>
<input  type="number" name="pope" bind:value={popeAmount} min="0" max={finalPlayersAmount -(mafiaAmount+amorAmount+policeAmount) }>

<label for="amor">Amor: </label>
<input  type="number" name="amor" bind:value={amorAmount}  min="0" max={finalPlayersAmount -(popeAmount+mafiaAmount+policeAmount) }>

<label for="police">Policja: </label>
<input  type="number" name="police" bind:value={policeAmount} min="0" max={finalPlayersAmount -(popeAmount+amorAmount+mafiaAmount) }> 
<button type="submit">Losuj</button>
</form>
{:else}
<h2>{actualPlayer}</h2>
{#if isRoleSeen == false}
<button on:click={showRole}>Pokaż rolę</button>
{:else}
<h2>{actualRole}</h2>
<button on:click={nextPlayer}>Dalej</button>
{/if}
{/if}



