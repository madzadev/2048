<script>
  let numbers = [
    [0, 0, 0, 0],
    [0, 2, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 2, 0],
  ];

  let colors = {
    2: "pale",
    4: "yellow",
    8: "orange",
    16: "tomato",
    32: "crimson",
  };

  const createNumber = () => {
    console.log("New number created");
  };

  const moveUp = () => {
    console.log("moved up");
  };

  const moveDown = () => {
    console.log("moved up");
  };

  const keyPress = (e) => {
    switch (e.keyCode) {
      case 38:
        console.log("You pressed up");
        break;
      case 40:
        console.log("You pressed down");
        break;
      case 37:
        console.log("You pressed left");
        break;
      case 39:
        console.log("You pressed right");
        break;
    }
  };
</script>

<style>
  h1 {
    text-align: center;
    margin: 30px 0;
    font-family: "Goldman", cursive;
    color: #776e65;
    font-size: 40px;
  }

  main {
    max-width: 600px;
    height: 600px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(4, 1fr);
    gap: 20px;
    /* border: 1px solid black; */
    background-color: #bbada0;
    padding: 20px;
    box-sizing: border-box;
    border-radius: 5px;
  }

  .tile {
    width: 100%;
    height: 100%;
    background-color: #eee4da;
    display: grid;
    place-items: center;
    font-size: 56px;
    border-radius: 5px;
    color: #776e65;
    font-weight: bold;
  }
</style>

<svelte:window on:keydown={keyPress} />

<h1>2048 Game</h1>
<main>
  {#each numbers as arr, i}
    {#each arr as num, i}
      <div class="tile">{num}</div>
    {/each}
  {/each}
</main>
