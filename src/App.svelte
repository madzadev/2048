<script>
  let game = {
    score: 0,
    best: 0,
  };

  let numbers = [
    [0, 2, 4, 8],
    [0, 2, 0, 0],
    [0, 0, 0, 0],
    [2, 0, 2, 0],
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

  const createNumber = () => {
    console.log("New number created");
  };

  const moveUp = () => {
    console.log("moved up");
  };

  const moveDown = () => {
    console.log("moved up");
  };

  const moveRight = () => {
    numbers.forEach((el, index) => {
      let arr = el.filter((num) => num !== 0);
      numbers[index] = arr;
      numbers[index].unshift(...Array(4 - arr.length).fill(0));
    });
    console.log(numbers);
  };

  const moveLeft = () => {
    numbers.forEach((el, index) => {
      let arr = el.filter((num) => num !== 0);

      console.log(arr);
      let arr2 = [];
      let summed = false;

      arr.forEach((el, index) => {
        if (!summed) {
          if (el === arr[index + 1]) {
            arr2.push(el * 2);
            summed = true;
          } else {
            arr2.push(el);
          }
        }
        summed = true;
      });

      console.log(arr2);

      // let sumArr = [];
      // let first = 0;
      // let second = 0;
      // let summed = false;

      // arr.forEach((el, index) => {
      //   if (index < arr.length - 1) {
      //     first = el;
      //     second = arr[index + 1];
      //     console.log(first, second);
      //   }
      //   if (!summed) {
      //     if (first != 0 && second != 0) {
      //       if (first == second) {
      //         sumArr.push(first + second);
      //         summed = true;
      //       } else {
      //         sumArr.push(first);
      //       }
      //     }
      //   }
      //   summed = false;
      // });

      numbers[index] = arr2;
      numbers[index].push(...Array(4 - arr2.length).fill(0));
    });
    // console.log(numbers);
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
        // console.log("You pressed left");
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
      <div class="tile">{num !== 0 ? num : ''}</div>
    {/each}
  {/each}
</main>
