<template>
  <div class="energy-bar">
    <svg
      width="100%"
      height="100"
      viewBox="0 -20 200 100"
      xmlns="http://www.w3.org/2000/svg"
    >
      <defs>
        <!-- דפוס פסים -->
        <pattern id="stripes" patternUnits="userSpaceOnUse" width="10" height="10" patternTransform="rotate(45)">
          <rect width="5" height="10" fill="#7FCD91" />
          <rect x="5" width="5" height="10" fill="#679D70" />
        </pattern>
        <!-- אנימציה להזזת הפסים -->
        <animate
          xlink:href="#stripes"
          attributeName="patternTransform"
          type="translate"
          from="0 0"
          to="10 0"
          begin="0s"
          dur="1s"
          repeatCount="indefinite"
        />
      </defs>

      <!-- רקע -->
      <rect width="100%" height="12" fill="#eeeeee" rx="6" ry="6" />

      <!-- פס מתקדם עם פסים -->
      <rect
        :width="clampedProgress + '%'"
        height="12"
        fill="url(#stripes)"
        rx="6"
        ry="6"
        class="energy-fill"
      />

      <!-- אייקון נע -->
      <image
          :x="(200 * clampedProgress / 100) -35"
        y="-20"
        width="65"
        height="65"
        xlink:href="../assets/media/prbarTank.png"
      />
    </svg>
  </div>
</template>

<script>
export default {
  name: 'EnergyProgressBar',
  props: {
    progress: {
      type: Number,
      default: 0
    }
  },
  computed: {
    clampedProgress() {
      return Math.max(0, Math.min(100, this.progress));
    }
  }
};
</script>

<style scoped>
.energy-bar {
  width: 80%;
  max-width: 700px;
  margin: auto;
}

.energy-fill {
  transition: width 0.4s ease;
}

image {
  transition: x 0.4s ease;
}
</style>

