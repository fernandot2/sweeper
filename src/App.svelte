<script>
  import Board from './lib/Board.svelte'
  let playing = false;
  $: start = !playing;
  let width = 5;
  let height = 5;
</script>

<main>
  <h1>Tic Tac Toe?</h1>
  {#if !playing}
    <div class="sizeSelect">
      <input type="number" bind:value={width}>
      <p>Width</p>
    </div>
    <label class="sizeSelect">
      <input type="number" bind:value={height}>
      <p>Height</p>
    </label>
    <button on:click={() => playing = true}> START </button>
  {/if}
  {#if playing}
    <Board bind:playing={playing} {width} {height}/>
  {/if}
</main>

<style>
  .sizeSelect {
    display: flex;
    height: fit-content;
    justify-content: center;
    margin: 10px 0px 10px 0px;
  }
  h1 {
    margin: 0px 0px 10px 0px
  }
  p {
    margin: 0;
  }
  input {
    width: 64px;
  }
</style>