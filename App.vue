<template>
  <div id="app">
    <canvas
      id="myCanvas"
      :width="this.canvasWidth"
      :height="this.canvasHeight"
    ></canvas>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      ratio: 4,
      originalWidth: 280,
      originalHeight: 300,
      startingPos: 0.75 * Math.PI,
      endPos: 2.25 * Math.PI,
      numbers: [0, 5, 10, 50, 100, 250, 500, 750, 1000],
    };
  },
  computed: {
    canvasWidth() {
      return this.originalWidth * this.ratio;
    },
    canvasHeight() {
      return this.originalHeight * this.ratio;
    },
  },
  methods: {
    drawNumbers() {
      var c = document.getElementById("myCanvas");
      const ctx = c.getContext("2d");

      var radius = this.canvasHeight / 2;
      ctx.translate(this.canvasWidth / 2, radius);

      radius = radius * 1;
      var ang;
      var num;

      ctx.font = 14 * this.ratio + "px arial";
      ctx.textBaseline = "middle";
      ctx.textAlign = "center";
      // 30 laipsniu tarp skaiciu
      for (num = 0; num < this.numbers.length; num++) {
        ang = (30 / 1.5) * -2 + (num * Math.PI) / Math.PI / 1.75;
        console.log(ang);
        ctx.rotate(ang);
        ctx.translate(0, -radius * 0.85);
        ctx.rotate(-ang);
        ctx.fillText(this.numbers[num].toString(), 0, 0);
        ctx.rotate(ang);
        ctx.translate(0, radius * 0.85);
        ctx.rotate(-ang);
      }
      console.log(radius);
      console.log(this.canvasWidth);
      ctx.translate(-this.canvasWidth / 2, -radius);
    },

    arrowCircle() {
      var c = document.getElementById("myCanvas");
      var context = c.getContext("2d");
      context.beginPath();
      context.arc(
        this.canvasWidth / 2,
        this.canvasHeight / 2,
        7.5 * this.ratio,
        0,
        2 * Math.PI
      );
      context.strokeStyle = "#1F1E1E";
      context.stroke();
      context.fillStyle = "#1F1E1E";
      context.fill();
    },
    arrowPointer() {
      var c = document.getElementById("myCanvas");
      var context = c.getContext("2d");
      context.beginPath();
      context.moveTo(
        this.canvasWidth / 2,
        this.canvasHeight / 2 - 5 * this.ratio
      );
      context.lineTo(
        this.canvasWidth / 2,
        this.canvasHeight / 2 + 5 * this.ratio
      );
      context.lineTo(
        this.canvasWidth / 2 - 112 * this.ratio,
        this.canvasHeight / 2,
        102 * this.ratio
      );
      context.closePath();
      context.strokeStyle = "red";
      context.stroke();
      context.fillStyle = "#1F1E1";
      context.fill();
    },

    drawHand(speed) {
      var pos =
        this.startingPos + ((this.endPos - this.startingPos) / 1000) * speed;
      var c = document.getElementById("myCanvas");
      const ctx = c.getContext("2d");
      ctx.translate(this.canvasWidth / 2, this.canvasHeight / 2);
      ctx.lineWidth = 5;
      ctx.beginPath();
      ctx.moveTo(0, 0);
      ctx.rotate(pos);
      ctx.translate(112 * this.ratio, 112 * this.ratio);
      // radius = radius * 0.9;
      ctx.lineTo(0, -112 * this.ratio);
      ctx.stroke();
    },

    circle1withStroke() {
      var c = document.getElementById("myCanvas");
      var context = c.getContext("2d");
      context.beginPath();
      context.arc(
        this.canvasWidth / 2,
        this.canvasHeight / 2,
        17.5 * this.ratio,
        0,
        2 * Math.PI
      );
      context.fillStyle = "#E9E9E9";
      context.fill();
      context.strokeStyle = "#DADADA";
      context.lineWidth = 2 * this.ratio;
      context.stroke();
      //reset
      context.lineWidth = 1 * this.ratio;
      context.strokeStyle = "black";
    },
    circle2() {
      var c = document.getElementById("myCanvas");
      var context = c.getContext("2d");
      context.beginPath();
      context.arc(
        this.canvasWidth / 2,
        this.canvasHeight / 2,
        35 * this.ratio,
        0,
        2 * Math.PI
      );
      context.fillStyle = "#FAFAFA";
      context.fill();
      context.strokeStyle = "#E9E9E9";
      context.stroke();
    },
    circle3() {
      var c = document.getElementById("myCanvas");
      var context = c.getContext("2d");
      context.beginPath();
      context.arc(
        this.canvasWidth / 2,
        this.canvasHeight / 2,
        53 * this.ratio,
        0,
        2 * Math.PI
      );
      context.fillStyle = "#FAFAFA";
      context.fill();
      context.strokeStyle = "#E9E9E9";
      context.stroke();
    },
    circle4() {
      var c = document.getElementById("myCanvas");
      var context = c.getContext("2d");
      context.beginPath();
      context.arc(
        this.canvasWidth / 2,
        this.canvasHeight / 2,
        72.5 * this.ratio,
        0,
        2 * Math.PI
      );
      context.fillStyle = "#FAFAFA";
      context.fill();
      context.strokeStyle = "#E9E9E9";
      context.stroke();
    },
    circle5withStroke() {
      var c = document.getElementById("myCanvas");
      var context = c.getContext("2d");
      context.beginPath();
      context.arc(
        this.canvasWidth / 2,
        this.canvasHeight / 2,
        102 * this.ratio,
        this.startingPos,
        this.endPos
      );
      context.strokeStyle = "#E9E9E9";
      context.lineWidth = 20 * this.ratio;
      // arcTo
      // context.lineCap = "round";
      context.stroke();
      //reset
      context.lineWidth = 1 * this.ratio;
      context.strokeStyle = "black";
    },
    circle5withStroke1() {
      var canvas = document.getElementById("myCanvas");
      var context = canvas.getContext("2d");
      context.beginPath();
      context.arc(
        this.canvasWidth / 2,
        this.canvasHeight / 2,
        (112 - 20) * this.ratio,
        this.startingPos,
        this.endPos
      );
      context.lineWidth = 2;
      context.strokeStyle = "red";
      context.stroke();
      context.closePath();

      context.beginPath();
      const p0 = {
        x: 112 * Math.cos(this.endPos) * this.ratio + this.canvasWidth / 2,
        y: 112 * Math.sin(this.endPos) * this.ratio + this.canvasHeight / 2,
      };
      const p1 = {
        x: 112 * Math.cos(this.endPos) * this.ratio + this.canvasWidth / 2,
        y: 112 * Math.sin(this.endPos) * this.ratio + this.canvasHeight / 2,
      };
      const p2 = {
        x: 112 * Math.cos(this.endPos) * this.ratio + this.canvasWidth / 2,
        y: 112 * Math.sin(this.endPos) * this.ratio + this.canvasHeight / 2,
      };
      context.moveTo(p0.x, p0.y);
      context.arcTo(p1.x - 10, p1.y + 10, p2.x - 21, p2.y, 15);
      context.lineTo(p2.x - 21, p2.y);
      context.lineTo(p0.x - 40, p0.y - 20);

      (p0.x = 112 * Math.cos(this.endPos) * this.ratio + this.canvasWidth / 2) -
        40,
        (p0.y =
          112 * Math.sin(this.endPos) * this.ratio + this.canvasHeight / 2) -
          20,
        (p1.x =
          112 * Math.cos(this.endPos) * this.ratio + this.canvasWidth / 2 - 10),
        (p1.y =
          112 * Math.sin(this.endPos) * this.ratio + this.canvasHeight / 2) +
          10,
        (p2.x =
          112 * Math.cos(this.endPos) * this.ratio + this.canvasWidth / 2) - 21,
        (p2.y =
          112 * Math.sin(this.endPos) * this.ratio + this.canvasHeight / 2),
        context.arcTo(p1.x - 42.5, p1.y - 30, p2.x - 42.5, p2.y - 42.5, 15);
      context.lineTo(p2.x - 42.5, p2.y - 42.5);

      context.stroke();
      context.beginPath();
      context.arc(
        this.canvasWidth / 2,
        this.canvasHeight / 2,
        112 * this.ratio,
        this.endPos,
        this.startingPos,
        true
      );

      (p0.x =
        112 * Math.cos(this.startingPos) * this.ratio + this.canvasWidth / 2),
        (p0.y =
          112 * Math.sin(this.startingPos) * this.ratio +
          this.canvasHeight / 2),
        (p1.x =
          112 * Math.cos(this.startingPos) * this.ratio + this.canvasWidth / 2),
        (p1.y =
          112 * Math.sin(this.startingPos) * this.ratio +
          this.canvasHeight / 2),
        (p2.x =
          112 * Math.cos(this.startingPos) * this.ratio + this.canvasWidth / 2),
        (p2.y =
          112 * Math.sin(this.startingPos) * this.ratio +
          this.canvasHeight / 2),
        context.arcTo(p1.x + 10, p1.y + 10, p2.x + 21, p2.y, 15);

      (p0.x =
        112 * Math.cos(this.startingPos) * this.ratio + this.canvasWidth / 2) -
        40,
        (p0.y =
          112 * Math.sin(this.startingPos) * this.ratio +
          this.canvasHeight / 2) + 20,
        (p1.x =
          112 * Math.cos(this.startingPos) * this.ratio +
          this.canvasWidth / 2 +
          10),
        (p1.y =
          112 * Math.sin(this.startingPos) * this.ratio +
          this.canvasHeight / 2) - 10,
        (p2.x =
          112 * Math.cos(this.startingPos) * this.ratio +
          this.canvasWidth / 2) + 21,
        (p2.y =
          112 * Math.sin(this.startingPos) * this.ratio +
          this.canvasHeight / 2),
        context.arcTo(p1.x + 42.5, p1.y - 30, p2.x + 42.5, p2.y - 42.5, 15);
      context.lineTo(p2.x + 42.5, p2.y - 42.5);
      context.stroke();
    },
  },
  },
  mounted() {
    this.drawNumbers();
    this.circle5withStroke();
    this.circle4();
    this.circle3();
    this.circle2();
    this.circle1withStroke();
    this.arrowCircle();
    this.arrowPointer();
    this.drawHand(500);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#myCanvas {
  border: 1px solid black;
}
</style>
