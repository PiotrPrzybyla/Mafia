<script>
    export let playerNumber
    export let playerName = ""
   
</script>
<label for="playerName">Nazwa {playerNumber+1 } gracza</label>
<input type="text" name="playerName" bind:value={playerName} required>
