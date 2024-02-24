<script>
  /*
    Function to calculate the luminance of a colour
  */
  function luminance(obj) {
    // iterate over colours in rgb object
    for (const value in obj) {
      // convert to 0-1
      let x = obj[value] / 255;

      // apply gamma correction
      x > 0.03928 ? (x = Math.pow((x + 0.055) / 1.055, 2.4)) : (x /= 12.92);

      // change value in copy
      obj[value] = x;
    }

    // return luminance
    return 0.2126 * obj.R + 0.7152 * obj.G + 0.0722 * obj.B;
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
    Function to CHECK the contrast between two colours
  */
  function checkContrast(x, y) {
    let l1 = luminance(x);
    let l2 = luminance(y);

    return contrast(l1, l2);
  }

  /*
    Function to round a number to 2 decimal places
  */
  function round(x) {
    return x % 1 !== 0 ? Number(x.toFixed(2)) : x;
  }

  let c1 = {
    R: 0,
    G: 0,
    B: 0,
  };

  let c2 = {
    R: 255,
    G: 255,
    B: 255,
  };

  // calculate contrast ratio
  let value = checkContrast(c1, c2);

  // format value
  value = round(value);
</script>

<h2>{value}:1</h2>
