<script>
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

  function contrast(x, y) {
    // return contrast ratio
    return Math.abs((x + 0.05) / (y + 0.05)).toFixed(2);
  }

  let c1 = {
    R: 62,
    G: 62,
    B: 62,
  };

  let c2 = {
    R: 15,
    G: 195,
    B: 119,
  };

  let l1 = luminance(c1);
  let l2 = luminance(c2);

  // variable for display
  let ratio = contrast(l2, l1);
</script>

<h2>{ratio}:1</h2>
