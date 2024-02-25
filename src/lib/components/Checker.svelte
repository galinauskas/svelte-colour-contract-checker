<script>
  /*
    Function to calculate the luminance of a colour
  */
  function luminance(arr) {
    // iterate over colours in rgb object
    for (let i = 0; i < 3; i++) {
      // convert to 0-1
      let x = arr[i] / 255;

      // apply gamma correction
      x > 0.03928 ? (x = Math.pow((x + 0.055) / 1.055, 2.4)) : (x /= 12.92);

      // change value in copy
      arr[i] = x;
    }

    // return luminance
    return 0.2126 * arr[0] + 0.7152 * arr[1] + 0.0722 * arr[2];
  }

  /*
    Function to CALCULATE the contrast between two colours
  */
  function contrast(x, y) {
    // divide into bigger figure
    return x > y
      ? Math.abs((x + 0.05) / (y + 0.05))
      : Math.abs((y + 0.05) / (x + 0.05));
  }

  /*
    Function to convert hex to rgb
  */
  function hexToRGB(str) {
    const rgb = [];

    // slice up string into pairs
    for (let i = 0; i < str.length; i += 2) {
      rgb.push(str.slice(i, i + 2));
    }

    // loop through each set of pairs
    for (const element of rgb) {
      // convert to number
      let num = parseInt(element, 16);

      // get index of set
      let index = rgb.indexOf(element);

      // change value in sets array
      rgb[index] = num;
    }

    return rgb;
  }

  /*
    Function to CHECK the contrast between two colours
  */
  function calculate() {
    // convert user input to rgb values
    let rgb1 = hexToRGB(userInput1);
    let rgb2 = hexToRGB(userInput2);

    // calculate luminance of each value
    let l1 = luminance(rgb1);
    let l2 = luminance(rgb2);

    // calculate contrast
    let result = contrast(l1, l2);

    // debuging
    console.log(`The luminance of colour 1 is ${l1}`);
    console.log(`The luminance of colour 2 is ${l2}`);
    console.log(`The contrast between the two colours is ${round(result)}:1`);

    return result;
  }

  /*
    Function to round a number to 2 decimal places
  */
  function round(x) {
    return x % 1 !== 0 ? Number(x.toFixed(2)) : x;
  }

  let userInput1 = "ffffff";
  let userInput2 = "000000";

  let result = calculate();
</script>

<form>
  <label for="colour1">Colour 1:</label>
  <input type="text" id="colour1" bind:value={userInput1} />

  <br /><br />

  <label for="colour2">Colour 2:</label>
  <input type="text" id="colour2" bind:value={userInput2} />

  <br /><br />

  <button on:click={calculate}>Calculate contrast</button>
</form>

<h2>The colour contrast ratio is {result}:1</h2>
