<script lang="ts">
  import P5, { type Sketch } from 'p5-svelte';

  let canvasWidth = 500;
  let canvasHeight = 1000;

  let horizontalNum = 12;
  let verticalNum = 22;

  let cubeSide = 30;
  let noiseScale = 0.01;

  const sketch: Sketch = (p5) => {
    p5.setup = () => {
      p5.createCanvas(canvasWidth, canvasHeight);
      // p5.angleMode(p5.DEGREES);
      p5.rectMode(p5.CENTER);

      let i = 0;
      for (i; i < horizontalNum * verticalNum; i++) {
        p5.push();

        let xPos = (i % horizontalNum) * cubeSide;
        let yPos = Math.floor(i / horizontalNum) * cubeSide;

        let rotNoise = p5.noise(xPos * noiseScale, yPos * noiseScale) - 0.5;
        let xNoise = p5.noise(xPos * noiseScale) - 0.5;
        let yNoise = p5.noise(yPos * noiseScale) - 0.5;
        console.log(rotNoise, xNoise, yNoise);

        p5.translate(xPos + cubeSide, yPos + cubeSide);
        p5.translate(xNoise, yNoise);
        p5.rotate(rotNoise);
        p5.square(0, 0, cubeSide);

        p5.pop();
      }
    };
    // p5.draw = () => {};
  };
</script>

<h1>Sketch</h1>
<P5 {sketch} debug />
