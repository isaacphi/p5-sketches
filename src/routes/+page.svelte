<script lang="ts">
  import P5, { type Sketch } from 'p5-svelte';

  let canvasWidth = 400;
  let canvasHeight = 800;

  let horizontalNum = 12;
  let verticalNum = 22;

  let cubeSide = 10;

  const sketch: Sketch = (p5) => {
    p5.setup = () => {
      p5.createCanvas(canvasWidth, canvasHeight);
      p5.angleMode(p5.DEGREES);

      let i = 0;
      for (i; i < horizontalNum * verticalNum; i++) {
        let xPos = (i % horizontalNum) * cubeSide;
        let yPos = Math.floor(i / horizontalNum) * cubeSide;
        console.log(Math.floor(i / verticalNum) * cubeSide);
        p5.rotate(i);
        p5.square(xPos, yPos, cubeSide);
      }
    };
    // p5.draw = () => {};
  };
</script>

<h1>Sketch</h1>
<P5 {sketch} debug />
