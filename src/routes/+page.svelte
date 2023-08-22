<script lang="ts">
  import P5, { type Sketch } from 'p5-svelte';

  let canvasWidth = 0;
  let canvasHeight = 0;
  let horizontalNum = 0;
  let verticalNum = 0;
  let noiseScale = 0.01;
  let noiseDisplacementScale = 1;
  let loopNum = 0;
  let cubeSide = 30;

  const sketch: Sketch = (p5) => {
    p5.setup = () => {
      canvasWidth = p5.windowWidth;
      canvasHeight = p5.windowHeight;

      horizontalNum = Math.floor(canvasWidth / cubeSide) - 1;
      verticalNum = Math.floor(canvasHeight / cubeSide) - 1;

      p5.createCanvas(canvasWidth, canvasHeight);
      // p5.angleMode(p5.DEGREES);
      p5.rectMode(p5.CENTER);
    };

    p5.draw = () => {
      p5.background(255);
      loopNum += 1;
      for (let i = 0; i < horizontalNum * verticalNum; i++) {
        p5.push();

        let xPos = (i % horizontalNum) * cubeSide;
        let yPos = Math.floor(i / horizontalNum) * cubeSide;

        let rotNoise = p5.noise((xPos + loopNum) * noiseScale, (yPos + loopNum) * noiseScale) - 0.5;
        let xNoise = (p5.noise((xPos + loopNum) * noiseScale) - 0.5) * i * noiseDisplacementScale;
        let yNoise = (p5.noise((yPos + loopNum) * noiseScale) - 0.5) * i * noiseDisplacementScale;

        p5.translate(xPos + cubeSide, yPos + cubeSide);
        // p5.translate(xNoise, yNoise);
        p5.rotate(rotNoise);
        p5.square(0, 0, cubeSide);

        p5.pop();
      }
    };

    // p5.windowResized = (p5) => {
    //   p5.resizeCanvas(canvasWidth, canvasHeight);
    // };
  };
</script>

<P5 {sketch} debug />
