<template>
  <div class="portfolio-creative">
    <!-- Title Above Canvas -->
    <h1 class="title">Release your creativity</h1>

    <!-- Drawing Canvas -->
    <div class="drawing-container">
      <canvas
        ref="drawingCanvas"
        width="600"
        height="400"
        @mousedown="startDrawing"
        @mousemove="draw"
        @mouseup="stopDrawing"
        @mouseout="stopDrawing"
        class="drawing-canvas"
      ></canvas>

      <!-- Color Picker & Clear Button -->
      <div class="controls">
        <button class="color-picker-btn">
          Color Picker
        </button>
        <input type="color" v-model="drawingColor" class="color-picker" />
        <button @click="clearCanvas" class="clear-canvas-btn">Clear Canvas</button>
      </div>
    </div>

    <!-- Subtitle Below Canvas -->
    <h2 class="subtitle">Draw something!</h2>

    <!-- Bubbles container under the canvas -->
    <div class="bubbles">
      <div
        v-for="n in 100"
        :key="n"
        class="bubble"
        :style="generateBubbleStyle()"
        @mouseover="removeBubble"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isDrawing: false,
      lastX: 0,
      lastY: 0,
      ctx: null,
      drawingColor: "#000000" // Default drawing color is black
    };
  },
  mounted() {
    // Get canvas context on mount
    this.ctx = this.$refs.drawingCanvas.getContext("2d");
  },
  methods: {
    startDrawing(event) {
      // Set isDrawing to true when mouse button is pressed
      this.isDrawing = true;
      this.lastX = event.offsetX;
      this.lastY = event.offsetY;
    },
    draw(event) {
      if (!this.isDrawing) return;

      // Get mouse position
      const mouseX = event.offsetX;
      const mouseY = event.offsetY;

      // Draw line from previous position to current position
      this.ctx.beginPath();
      this.ctx.moveTo(this.lastX, this.lastY);
      this.ctx.lineTo(mouseX, mouseY);
      this.ctx.strokeStyle = this.drawingColor; // Use selected color for drawing
      this.ctx.lineWidth = 2; // Set line width
      this.ctx.lineCap = "round"; // Rounded line ends
      this.ctx.stroke();

      // Update last position
      this.lastX = mouseX;
      this.lastY = mouseY;
    },
    stopDrawing() {
      this.isDrawing = false;
    },
    clearCanvas() {
      // Clear the entire canvas
      this.ctx.clearRect(0, 0, this.$refs.drawingCanvas.width, this.$refs.drawingCanvas.height);
    },
    // Generate style for bubbles
    generateBubbleStyle() {
      const size = `${Math.random() * 50 + 10}px`;
      const shape = Math.random() > 0.5 ? '50%' : `${Math.random() * 50 + 50}% ${Math.random() * 50 + 50}%`;
      const animationDuration = `${Math.random() * 10 + 5}s`; // Random float-up duration
      const animationDelay = `${Math.random() * 5}s`; // Random delay to stagger animation

      return {
        width: size,
        height: size,
        borderRadius: shape,
        animationDuration,
        animationDelay,
        left: `${Math.random() * 100}%`, // Random horizontal position
      };
    },
    // Remove bubble when hovered
    removeBubble(event) {
      // Make the bubble disappear when hovered
      event.target.style.opacity = '0';
      setTimeout(() => {
        event.target.style.display = 'none'; // Hide the bubble after it disappears
      }, 300); // Allow for fade effect before removing the element
    },
  },
};
</script>

<style scoped>
.portfolio-creative {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #f4f4f4;
  text-align: center;
  position: relative; /* Ensure bubbles are under the form */
}

.title {
  font-size: 2rem;
  font-weight: 700;
  color: #333;
  margin-bottom: 20px; /* Added margin for spacing */
}

.drawing-container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #007bff; /* Blue background */
  padding: 20px;
  border-radius: 10px;
  max-width: 650px; /* Limit the width */
  width: 100%; /* Full width for responsiveness */
  margin-bottom: 20px; /* Space between the canvas and the subtitle */
  z-index: 2; /* Ensure it is above the bubbles */
}

.drawing-canvas {
  border: 2px solid #ccc;
  cursor: crosshair; /* Makes the cursor a crosshair for more precise drawing */
  background-color: #fff; /* White background for the canvas */
  margin-bottom: 20px;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.color-picker-btn {
  background-color: #007bff;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
}

.color-picker-btn:hover {
  background-color: #0056b3;
}

.color-picker {
  padding: 5px;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  cursor: pointer;
}

.clear-canvas-btn {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #28a745;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.clear-canvas-btn:hover {
  background-color: #218838;
}

.subtitle {
  font-size: 1.5rem; /* Smaller size for "Draw something!" */
  font-weight: 500;
  color: #555;
  margin-top: 20px; /* Space below the canvas */
}

/* Bubbles */
.bubbles {
  position: fixed;
  bottom: 20px; /* Position bubbles just below the canvas */
  left: 0;
  width: 100%; /* Cover full screen width */
  z-index: 1; /* Ensure bubbles are beneath the drawing area */
}

.bubble {
  position: absolute;
  background: rgba(0, 123, 255, 0.4);
  animation: floatUp linear infinite;
}

.bubble:nth-child(odd) {
  background: rgba(30, 144, 255, 0.6);
}

.bubble:nth-child(even) {
  background: rgba(0, 86, 179, 0.8);
}

@keyframes floatUp {
  0% {
    transform: translateY(0); /* Start at the bottom */
    opacity: 0.8;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    transform: translateY(-100vh); /* Move up out of view */
    opacity: 0;
  }
}
</style>
