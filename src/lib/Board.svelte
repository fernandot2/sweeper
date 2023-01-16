<script>
  export let playing;
  export let width;
  export let height;  
  let win = false;
  let board = [];
  let turn = 'X';
  let colour = 'red'
  for(let i = 0; i < height; i++){
    let row = [];
    for(let j = 0; j < width; j++){
      row.push('');
    }
    board.push(row);
  }
  function playCell(colIndex, celIndex){
    let cellToChange = board[colIndex][celIndex];
    if(cellToChange == '' && !win){
      board[colIndex][celIndex] = turn;
      turn == 'X' ? turn = 'O' : turn = 'X';
    }
    checkForWin();
    if(win){
      colour = 'blue'
    }
  }
  
  function checkForWin(){
    board.forEach((row, rowIndex) => {
      row.forEach((cell, cellIndex) => {
        if(cell != ''){
          //Horizontal
          if(cellIndex < row.length-2){
            if(cell == row[cellIndex+1] && cell == row[cellIndex+2]){
              win = true;
            }
          }
          //Vertical
          if(rowIndex > 1){
            if(cell == board[rowIndex-1][cellIndex] && cell == board[rowIndex-2][cellIndex]){
              win = true;
            }
          }
          //Diagonal
          if(rowIndex > 1){
            // (/)
            if(cellIndex < row.length-2){
              if(cell == board[rowIndex-1][cellIndex+1] && cell == board[rowIndex-2][cellIndex+2]){
                win = true;
              }
            }
            // (\)
            if(cellIndex > 1){
              if(cell == board[rowIndex-1][cellIndex-1] && cell == board[rowIndex-2][cellIndex-2]){
                win = true;
              }
            }
          }
        }
      })
    })
  }

  function reset(){
    win = false;
    colour = 'red';
    board.forEach((row, rowIndex) => {
      row.forEach((cell, cellIndex) => {
        board[rowIndex][cellIndex] = ''
      });
    });
  }
</script>
<div>
  {#each board as col, colIndex}
    <div style="display: flex">
      {#each col as cell, celIndex}
        <div on:click={() => playCell(colIndex, celIndex)} style="color: {colour}" class="gameCell">{cell}</div>
      {/each}
    </div>
  {/each}
</div>
{#if win}
  <button on:click={() => playing = false}>Back to Menu</button>
  <button on:click={reset}>Reset</button>
{/if}

<style>
  .gameCell {
    width: 64px;
    height: 32px;
    background-color: #383838;
    border: 1px;
    border-color: #323232;
    border-style: solid;
    text-align: center;
  }
</style>