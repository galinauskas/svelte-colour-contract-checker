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

    display = round(result);

    updatePreview();

    return result;
  }

  /*
    Function to update the preview colours
  */
  function updatePreview() {
    previewFG = "#" + userInput1;
    previewBG = "#" + userInput2;
  }

  /*
    Function to round a number to 2 decimal places
  */
  function round(x) {
    return x % 1 !== 0 ? Number(x.toFixed(2)) : x;
  }

  let userInput1 = "ffffff";
  let userInput2 = "000000";

  let previewFG = "#" + userInput1;
  let previewBG = "#" + userInput2;

  let display = 21;
</script>

<form>
  <h1>Contrast Checker</h1>

  <div class="colourInput">
    <label for="colour1">Foreground colour</label>
    <input
      type="text"
      id="colour1"
      bind:value={userInput1}
      placeholder="#ffffff"
    />
    <div class="preview" style="--color: {previewFG}"></div>
  </div>

  <div class="colourInput">
    <label for="colour1">Background colour</label>
    <input
      type="text"
      id="colour2"
      bind:value={userInput2}
      placeholder="#000000"
    />
    <div class="preview" style="--color: {previewBG}"></div>
  </div>

  <button on:click={calculate}>Calculate contrast</button>
</form>

<span id="result">The colour contrast ratio is {display}:1</span>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap");
  * {
    box-sizing: border-box;
    margin: none;
    padding: none;
    font-family: Inter, sans-serif;
  }

  #result {
    display: flex;
    justify-content: center;
    margin-top: 1rem;
  }

  form {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 256px;
    height: 310px;
    border-radius: 0.5rem;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
    margin: auto;
    margin-top: 2rem;
  }

  h1 {
    font-size: 1.5rem;
    margin: 0;
    margin-bottom: 1rem;
  }

  .colourInput {
    display: flex;
    flex-direction: row;
    margin-bottom: 0.8rem;
    flex-wrap: wrap;
    width: 200px;
  }

  label {
    margin-bottom: 0.2rem;
    width: 100%;
    font-size: 0.8rem;
  }

  input {
    padding: 0.5rem;
    border-radius: 0.5rem;
    border: 1px solid #c6c6c6;
    background-color: #f6f6f6;
    margin-right: 0.5rem;
    width: 158px;
  }

  button {
    padding: 0.5rem 1rem;
    color: #fff;
    cursor: pointer;
    width: 200px;
    height: 50px;
    margin-top: 0.8rem;

    font-size: 14px;
    font-weight: 700;
    letter-spacing: 0.02rem;

    background: linear-gradient(180deg, #000000 0%, rgba(0, 0, 0, 0.75) 100%);
    border-width: 3px 3px 0px 3px;
    border-style: solid;
    border-color: #414141;
    border-radius: 0.5rem;
  }

  .preview {
    width: 33px;
    height: 33px;
    background-color: var(--color);
    border-radius: 0.5rem;
    border: 1px solid #000;
  }
</style>
