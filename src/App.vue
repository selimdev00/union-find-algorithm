<script setup lang="ts">
import { onMounted, ref } from "vue";

const canvas = ref<HTMLCanvasElement | null>(null);

class UnionFind {
  constructor() {
    this.ctx = canvas.value?.getContext("2d");
    this.ctx.fillStyle = "#FFFFFF";

    this.dot = {
      radius: 5,
      gap: 20,
    };

    this.input = [
      [0, 1],
      [1, 2],
      [3, 4],
    ];
  }

  init() {
    this.drawGrid();
  }

  drawGrid() {
    for (let i = 0; i < 10; i++) {
      this.drawItem((i + 1) * this.dot.gap, 10);
    }
  }

  drawItem(x, y) {
    this.ctx.beginPath();
    this.ctx.arc(x, y, this.dot.radius, 0, 2 * Math.PI);
    this.ctx.fill();
    this.ctx.closePath();
  }

  drawLine() {
    this.ctx.beginPath();
    this.ctx.moveTo(50, 50); // starting point (x, y)
    this.ctx.lineTo(200, 200); // ending point (x, y)
    this.ctx.strokeStyle = "white"; // line color
    this.ctx.lineWidth = 2; // line width
    this.ctx.stroke(); // draw the line
  }
}

onMounted(() => {
  if (!canvas.value) return;

  canvas.value.width = window.innerWidth;
  canvas.value.height = window.innerHeight;

  const unionFind = new UnionFind();

  unionFind.init();
});
</script>

<template>
  <div>
    <canvas id="canvas" ref="canvas"></canvas>
  </div>
</template>
