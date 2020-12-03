<script>
  let game = {
    score: 0,
    best: 0,
  };

  let numbers = [
    [0, 0, 0, 0],
    [0, 0, 2, 0],
    [0, 0, 0, 0],
    [2, 2, 2, 0],
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
  };

  const rand = () => {
    let flat = numbers.flat();
    let zeroPos = [];
    flat.forEach((el, index) => {
      if (el === 0) {
        zeroPos.push(index);
      }
    });
    console.log(flat);
    console.log(zeroPos);
    let rand = Math.floor(Math.random() * Math.floor(zeroPos.length));
    let num = zeroPos[rand];

    console.log(num);

    let arrPos = Math.floor(num / 4);
    let numPos = num - arrPos * 4;
    console.log(arrPos);
    console.log(numPos);

    if (arrPos != NaN && numPos != NaN) {
      console.log("this runs");
      numbers[arrPos][numPos] = 2;
    }

    if (zeroPos.length === 0) {
      console.log("Game over");
    }
  };

  let vArr = [[], [], [], []];

  const moveUp = () => {
    vArr = [[], [], [], []];
    numbers.forEach((el, index) => {
      el.forEach((el, index) => {
        vArr[index].push(el);
      });
    });

    vArr.forEach((el, index) => {
      let arr = el.filter((num) => num !== 0);
      let arr2 = [];
      let summed = false;
      arr.forEach((el, index) => {
        if (el === arr[index + 1]) {
          if (!summed || (summed && index == 2)) {
            arr2.push(el * 2);
            game.score += el * 2;
          }
          summed = true;
        } else {
          !summed && arr2.push(el);
          summed = false;
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
  };

  const moveDown = () => {
    vArr = [[], [], [], []];
    numbers.forEach((el, index) => {
      el.forEach((el, index) => {
        vArr[index].push(el);
      });
    });

    vArr.forEach((el, index) => {
      let arr = el.filter((num) => num !== 0);
      let arr2 = [];
      let summed = false;
      arr.forEach((el, index) => {
        if (el === arr[index + 1]) {
          if (!summed || (summed && index == 2)) {
            arr2.push(el * 2);
            game.score += el * 2;
          }
          summed = true;
        } else {
          !summed && arr2.push(el);
          summed = false;
        }
      });

      vArr[index] = arr2;
      vArr[index].unshift(...Array(4 - arr2.length).fill(0));
    });

    vArr.forEach((el, index1) => {
      el.forEach((el, index2) => {
        numbers[index2][index1] = el;
      });
    });
  };

  const moveRight = () => {
    let original = numbers.map((x) => x);
    let modified = [];

    numbers.forEach((el, index) => {
      let arr = el.filter((num) => num !== 0);
      let arr2 = [];
      let summed = false;

      arr.forEach((el, index) => {
        if (el === arr[index + 1]) {
          if (!summed || (summed && index == 2)) {
            arr2.push(el * 2);
            game.score += el * 2;
          }
          summed = true;
        } else {
          !summed && arr2.push(el);
          summed = false;
        }
      });
      modified.push(arr2);
      numbers[index] = arr2;
      numbers[index].unshift(...Array(4 - arr2.length).fill(0));
    });

    // console.log("initial1: " + original);
    // console.log("initial2: " + modified);

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

      let summed = false;

      arr.forEach((el, index) => {
        if (el === arr[index + 1]) {
          if (!summed || (summed && index == 2)) {
            arr2.push(el * 2);
            game.score += el * 2;
          }
          summed = true;
        } else {
          !summed && arr2.push(el);
          summed = false;
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
        rand();
        break;
      case 40:
        console.log("You pressed down");
        moveDown();
        rand();
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
    font-size: 56px;
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
</style>

<svelte:window on:keydown={keyPress} />

<h1>2048 Game</h1>
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
<h1>Score: {game.score}</h1>
<button on:click={reset}>New game</button>
