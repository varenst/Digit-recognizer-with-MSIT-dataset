<template>
  <h1>Digit recognition with MSIT</h1>

  <div id="toolbar">
    <section class="drawing-board">
      <canvas id="drawing-board"></canvas>
    </section>
  </div>

  <section class="info-panel">
    <div class="info-text">
      Please draw a digit above. Click reset to clear the canvas.
    </div>
    <button class="reset-button" @click="resetCanvas">Reset</button>
  </section>
</template>

<script>
export default {
  methods: {
    resetCanvas() {
      const canvas = document.getElementById("drawing-board");
      const ctx = canvas.getContext("2d");
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.fillStyle = "white";
      ctx.fillRect(0, 0, canvas.width, canvas.height);
    }
  },
  mounted() {
    const canvas = document.getElementById("drawing-board");
    const ctx = canvas.getContext("2d");

    canvas.width = 800;
    canvas.height = 300;

    ctx.fillStyle = "white";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    let isPainting = false;
    const lineWidth = 5;

    const draw = (e) => {
      if (!isPainting) return;
      ctx.lineWidth = lineWidth;
      ctx.lineCap = 'round';
      ctx.lineTo(e.offsetX, e.offsetY);
      ctx.stroke();
    };

    canvas.addEventListener('mousedown', () => {
      isPainting = true;
    });

    canvas.addEventListener('mouseup', () => {
      isPainting = false;
      ctx.stroke();
      ctx.beginPath();
    });

    canvas.addEventListener('mousemove', draw);
  }
}

</script>

<style scoped>
h1 {
  text-align: center;
  font-family: Arial, sans-serif;
  font-weight: bold;
  font-size: 50px;
  padding-top: 5%;
}

.drawing-board {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0;
}

#drawing-board {
  background-color: #f5f5f5;
  border: 2px solid black;
  border-radius: 8px;
  width: 800px;
  height: 300px;
}

.info-panel {
  width: 800px;
  margin: 20px auto;
  background-color: #e0e0e0;
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  position: relative;
}

.info-text {
  font-size: 26px;
  color: #333;
  margin-bottom: 15px;
  font-family: Arial, sans-serif;
}

.reset-button {
  padding: 10px 20px;
  background-color: #0b7df0;
  color: #ffffff;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.reset-button:hover {
  background-color: #495057;
}
</style>
