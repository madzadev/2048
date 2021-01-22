<script>
  let game = {
    score: 0,
    best: 0,
  };

  let numbers = [
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
  ];

  let colors = {
    2: "pale",
    4: "yellow",
    8: "orange",
    16: "tomato",
    32: "crimson",
  };

  const reset = () => {
    console.log("game reseted");
    numbers = [
      [0, 0, 0, 0],
      [0, 0, 0, 0],
      [0, 0, 0, 0],
      [0, 0, 0, 0],
    ];
    game.score = 0;
    rand();
    rand();
  };

  const rand = () => {
    let flat = numbers.flat();
    let zeroPos = [];
    flat.forEach((el, index) => {
      if (el === 0) {
        zeroPos.push(index);
      }
    });

    let rand = Math.floor(Math.random() * Math.floor(zeroPos.length));
    let num = zeroPos[rand];

    let arrPos = Math.floor(num / 4);
    let numPos = num - arrPos * 4;

    if (arrPos != NaN && numPos != NaN) {
      numbers[arrPos][numPos] = 2;
    }

    if (!zeroPos) {
      console.log("Game over");
    }
  };

  rand();
  rand();

  const gameOver = (arr) => {
    if (!arr.flat().includes(0)) {
      console.log("game over");
    }
  };

  let vArr = [[], [], [], []];

  const moveUp = () => {
    let original = JSON.parse(JSON.stringify(numbers));

    vArr = [[], [], [], []];
    numbers.forEach((el, index) => {
      el.forEach((el, index) => {
        vArr[index].push(el);
      });
    });

    vArr.forEach((el, index) => {
      let arr = el.filter((num) => num !== 0);
      let arr2 = [];
      arr.forEach((el, index) => {
        if (el === arr[index + 1]) {
          arr.splice(index + 1, 1);
          arr2.push(el * 2);
          game.score += el * 2;
        } else {
          arr2.push(el);
        }
      });

      vArr[index] = arr2;
      vArr[index].push(...Array(4 - arr2.length).fill(0));
    });

    vArr.forEach((el, index1) => {
      el.forEach((el, index2) => {
        numbers[index2][index1] = el;
      });
    });

    if (JSON.stringify(original) !== JSON.stringify(numbers)) {
      rand();
    }

    gameOver(numbers);
  };

  const moveDown = () => {
    let original = JSON.parse(JSON.stringify(numbers));

    vArr = [[], [], [], []];
    numbers.forEach((el, index) => {
      el.forEach((el, index) => {
        vArr[index].push(el);
      });
    });

    vArr.forEach((el, index) => {
      let arr = el.filter((num) => num !== 0).reverse();
      let arr2 = [];
      arr.forEach((el, index) => {
        if (el === arr[index + 1]) {
          arr.splice(index + 1, 1);
          arr2.push(el * 2);
          game.score += el * 2;
        } else {
          arr2.push(el);
        }
      });

      arr2.reverse();
      vArr[index] = arr2;
      vArr[index].unshift(...Array(4 - arr2.length).fill(0));
    });

    vArr.forEach((el, index1) => {
      el.forEach((el, index2) => {
        numbers[index2][index1] = el;
      });
    });

    if (JSON.stringify(original) !== JSON.stringify(numbers)) {
      rand();
    }

    gameOver(numbers);
  };

  const moveRight = () => {
    let original = numbers.map((x) => x);
    let modified = [];

    numbers.forEach((el, index) => {
      let arr = el.filter((num) => num !== 0).reverse();
      let arr2 = [];

      arr.forEach((el, index) => {
        if (el === arr[index + 1]) {
          arr.splice(index + 1, 1);
          arr2.push(el * 2);
          game.score += el * 2;
        } else {
          arr2.push(el);
        }
      });

      arr2.reverse();
      modified.push(arr2);
      numbers[index] = arr2;
      numbers[index].unshift(...Array(4 - arr2.length).fill(0));
    });

    console.log("initial1: " + original);
    console.log("initial2: " + modified);

    if (JSON.stringify(original) !== JSON.stringify(modified)) {
      rand();
    }
  };

  const moveLeft = () => {
    let original = numbers.map((x) => x);
    let modified = [];

    numbers.forEach((el, index) => {
      let arr = el.filter((num) => num !== 0);
      let arr2 = [];

      arr.forEach((el, index) => {
        if (el === arr[index + 1]) {
          arr.splice(index + 1, 1);
          arr2.push(el * 2);
          game.score += el * 2;
        } else {
          arr2.push(el);
        }
      });

      modified.push(arr2);
      numbers[index] = arr2;
      numbers[index].push(...Array(4 - arr2.length).fill(0));
    });

    if (JSON.stringify(original) !== JSON.stringify(modified)) {
      rand();
    }
  };

  const keyPress = (e) => {
    switch (e.keyCode) {
      case 38:
        console.log("You pressed up");
        moveUp();
        break;
      case 40:
        console.log("You pressed down");
        moveDown();
        break;
      case 37:
        console.log("You pressed left");
        moveLeft();
        break;
      case 39:
        console.log("You pressed right");
        moveRight();
        break;
    }
  };
</script>

<style>
.header {
    display: grid;
    grid-template-columns: 1fr auto auto;
    max-width: 500px;
    margin: 0 auto;
    align-items: center;
  }
  .title {
    font-size:60px;
    text-align: center;
    margin: 30px 0;
    font-family: "Goldman", cursive;
    color: #776e65;
  }
  .score-box {
    background-color:  #C9BBAE;
    padding: 3px 0px;
    text-align: center;
    width: 100px;
    height:65px;
    border-radius: 5px;
  }

  .score-title{
font-size:20px;
color:  #eee4da;
  }

  .score-number {
    font-size:30px;
    color: white;
  }

  .second{
margin-left: 10px;
  } 

  main {
    max-width: 500px;
    min-height: 500px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(4, 1fr);
    gap: 20px;
    background-color: #bbada0;
    padding: 20px;
    box-sizing: border-box;
    border-radius: 5px;
  }

  .tile {
    font-family: "Goldman", cursive;
    width: 100%;
    height: 100%;
    background-color: #c9bbae;
    display: grid;
    place-items: center;
    font-size: 3em;
    border-radius: 5px;
    color: #776e65;
    font-weight: bold;
  }

  .two {
    background-color: #eee4da;
  }

  .four {
    background-color: #ede0c8;
  }

  .eight {
    background-color: #f2b179;
  }

  .sixteen {
    background-color: #f59563;
  }

  .thirtytwo {
    background-color: #f67c60;
  }

  .sixtyfour {
    background-color: #f65e3b;
  }

  .onetwoeight {
    background-color: #edcf73;
  }

  .twofivesix {
    background-color: #edcc62;
  }

  .fiveonetwo {
    background-color: #edc850;
  }

  .onezerotwofour {
    background-color: #edc53f;
  }

  .twozerofoureight {
    background-color: #edc22d;
  }

  .reset-box {
    max-width: 500px;
    margin: 20px auto;
    color: #776e65;
    text-align: right;
    padding: 0 5px;
  }

  .reset-box h1:hover {
color: #bbada0;
cursor: pointer;
  }

  .rules-box {
     max-width: 500px;
    margin: 0 auto;
  }
  
</style>

<svelte:window on:keydown={keyPress} />


<div class="header">
  <h1 class="title">2048</h1>
  <div class="score-box">
    <p class="score-title">Score</p>
    <p class="score-number">{game.score}</p>
  </div>
  <div class="score-box second">
    <p class="score-title">Best</p>
    <p class="score-number">{game.best}</p>
  </div>

</div>
<main>
  {#each numbers as arr, i}
    {#each arr as num, i}
      <div
        class="tile {num === 2 ? 'two' : num === 4 ? 'four' : num === 8 ? 'eight' : num === 16 ? 'sixteen' : num === 32 ? 'thirtytwo' : num === 64 ? 'sixtyfour' : num === 128 ? 'onetwoeight' : num === 256 ? 'twofivesix' : num === 512 ? 'fiveonetwo' : num === 1024 ? 'onezerotwofour' : num === 2048 ? 'twozerofoureight' : ''}">
        {num !== 0 ? num : ''}
      </div>
    {/each}
  {/each}
</main>
<div class="reset-box">
<h1 on:click={reset}>Reset</h1>
</div>
<div class="rules-box">
  <p>HOW TO PLAY: Use your arrow keys to move the tiles. Tiles with the same number merge into one when they touch. Add them up to reach 2048!</p>
</div>



