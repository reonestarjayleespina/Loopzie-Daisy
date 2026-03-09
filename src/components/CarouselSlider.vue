<template>
  <div class="carousel-container" @mouseenter="pauseAutoplay" @mouseleave="resumeAutoplay">
    <div class="carousel-wrapper">
      <transition-group name="slide" tag="div" class="carousel-track">
        <div
          v-for="(image, index) in images"
          :key="image"
          v-show="index === currentIndex"
          class="carousel-slide"
        >
          <div class="image-wrapper">
            <img :src="image" :alt="`Crochet product ${index + 1}`" />
          </div>
        </div>
      </transition-group>

      <!-- Progress bar -->
      <div class="progress-bar">
        <div class="progress-fill" :style="{ width: progressWidth + '%' }"></div>
      </div>

      <div class="carousel-dots">
        <button
          v-for="(image, index) in images"
          :key="`dot-${index}`"
          :class="['dot', { active: index === currentIndex }]"
          @click="goToSlide(index)"
          :aria-label="`Go to slide ${index + 1}`"
        ></button>
      </div>

      <button class="carousel-btn prev" @click="prevSlide" aria-label="Previous slide">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <polyline points="15 18 9 12 15 6"></polyline>
        </svg>
      </button>

      <button class="carousel-btn next" @click="nextSlide" aria-label="Next slide">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <polyline points="9 18 15 12 9 6"></polyline>
        </svg>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const images = [
  new URL('../assets/crochet daisy.jpg', import.meta.url).href,
  new URL('../assets/crochet flower collection.jpg', import.meta.url).href,
  new URL('../assets/crochet hat.jpg', import.meta.url).href,
  new URL('../assets/crochet rose.jpg', import.meta.url).href,
  new URL('../assets/crochet sunflower.jpg', import.meta.url).href,
  new URL('../assets/crochet tulip.jpg', import.meta.url).href,
  new URL('../assets/273061423_699449714759135_3104869418196088709_n.jpg', import.meta.url).href,
  new URL('../assets/321997104_577758917697058_1891540247058298593_n.jpg', import.meta.url).href,
  new URL('../assets/322724239_532964875534753_1703453249017199933_n.jpg', import.meta.url).href,
  new URL('../assets/330273332_1166437310702151_528216404373386284_n.jpg', import.meta.url).href,
  new URL('../assets/330284991_1218376562132615_123624182422985914_n.jpg', import.meta.url).href,
  new URL('../assets/330759586_752224479626789_5326876764546456754_n.jpg', import.meta.url).href,
  new URL('../assets/340687006_1189173738464452_3132342238833481619_n.jpg', import.meta.url).href,
  new URL('../assets/340714627_597248189014623_6489738778497008783_n.jpg', import.meta.url).href,
  new URL('../assets/354470958_1353227418561483_1965761626735820787_n.jpg', import.meta.url).href,
  new URL('../assets/384552219_1553341538403326_5760519036536623687_n.jpg', import.meta.url).href,
]

const currentIndex = ref(0)
const progressWidth = ref(0)
const isPaused = ref(false)
let autoplayInterval = null
let progressInterval = null

const AUTOPLAY_DURATION = 4000 // 4 seconds per slide
const PROGRESS_UPDATE_INTERVAL = 20 // Update progress every 20ms

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % images.length
  progressWidth.value = 0
}

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + images.length) % images.length
  progressWidth.value = 0
}

const goToSlide = (index) => {
  currentIndex.value = index
  progressWidth.value = 0
  // Reset autoplay timer when user manually navigates
  if (autoplayInterval) {
    clearInterval(autoplayInterval)
    clearInterval(progressInterval)
    startAutoplay()
  }
}

const pauseAutoplay = () => {
  isPaused.value = true
  if (autoplayInterval) {
    clearInterval(autoplayInterval)
  }
  if (progressInterval) {
    clearInterval(progressInterval)
  }
}

const resumeAutoplay = () => {
  isPaused.value = false
  startAutoplay()
}

const startAutoplay = () => {
  progressWidth.value = 0

  // Update progress bar
  progressInterval = setInterval(() => {
    if (!isPaused.value) {
      progressWidth.value += 100 / (AUTOPLAY_DURATION / PROGRESS_UPDATE_INTERVAL)
      if (progressWidth.value >= 100) {
        progressWidth.value = 100
      }
    }
  }, PROGRESS_UPDATE_INTERVAL)

  // Change slide
  autoplayInterval = setInterval(() => {
    if (!isPaused.value) {
      nextSlide()
    }
  }, AUTOPLAY_DURATION)
}

onMounted(() => {
  startAutoplay()
})

onUnmounted(() => {
  if (autoplayInterval) {
    clearInterval(autoplayInterval)
  }
  if (progressInterval) {
    clearInterval(progressInterval)
  }
})
</script>

<style scoped>
.carousel-container {
  width: 100%;
  height: 100vh;
  margin: 0;
  overflow: hidden;
  box-sizing: border-box;
}

.carousel-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at top, #fff8d8 0%, var(--color-cream) 45%, #f6e7ff 100%);
  overflow: hidden;
}

.carousel-track {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.carousel-slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 80px;
  box-sizing: border-box;
}

.image-wrapper {
  position: relative;
  max-width: 100%;
  max-height: 80vh;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
  animation: kenBurns 4s ease-out forwards;
}

@keyframes kenBurns {
  0% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

.carousel-slide img {
  max-width: 100%;
  max-height: 80vh;
  object-fit: contain;
  display: block;
  width: auto;
  height: auto;
}

/* Progress bar */
.progress-bar {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: rgba(89, 13, 130, 0.14);
  z-index: 15;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--color-yellow), #ffe883 55%, var(--color-purple));
  transition: width 0.05s linear;
  box-shadow: 0 0 12px rgba(89, 13, 130, 0.25);
}

/* Slide transitions */
.slide-enter-active {
  animation: slideInZoom 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.slide-leave-active {
  animation: slideOutZoom 0.6s ease-in;
}

@keyframes slideInZoom {
  0% {
    opacity: 0;
    transform: translateX(100%) scale(0.8) rotate(5deg);
  }
  100% {
    opacity: 1;
    transform: translateX(0) scale(1) rotate(0deg);
  }
}

@keyframes slideOutZoom {
  0% {
    opacity: 1;
    transform: translateX(0) scale(1) rotate(0deg);
  }
  100% {
    opacity: 0;
    transform: translateX(-100%) scale(0.8) rotate(-5deg);
  }
}

/* Navigation buttons */
.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.96);
  border: none;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  z-index: 10;
  color: var(--color-purple);
  margin: 0;
  box-shadow: 0 10px 24px rgba(89, 13, 130, 0.2);
}

.carousel-btn:hover {
  background: var(--color-yellow);
  color: var(--color-purple);
  transform: translateY(-50%) scale(1.15);
  box-shadow: 0 14px 28px rgba(89, 13, 130, 0.25);
}

.carousel-btn:active {
  transform: translateY(-50%) scale(0.95);
}

.carousel-btn.prev {
  left: 20px;
}

.carousel-btn.next {
  right: 20px;
}

/* Dots navigation */
.carousel-dots {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 12px;
  z-index: 10;
  padding: 12px 20px;
  background: rgba(89, 13, 130, 0.2);
  backdrop-filter: blur(10px);
  border-radius: 30px;
}

.dot {
  position: relative;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  border: 2px solid rgba(255, 255, 255, 0.85);
  background: rgba(255, 255, 255, 0.45);
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
  padding: 0;
}

.dot:hover {
  background: var(--color-yellow);
  transform: scale(1.3);
  border-color: #ffffff;
}

.dot.active {
  background: var(--color-yellow);
  width: 35px;
  border-radius: 8px;
  border-color: var(--color-purple);
  box-shadow: 0 0 15px rgba(89, 13, 130, 0.35);
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .carousel-wrapper {
    height: 100vh;
  }

  .carousel-slide {
    padding: 0 60px;
  }

  .carousel-btn {
    width: 40px;
    height: 40px;
  }

  .carousel-btn.prev {
    left: 10px;
  }

  .carousel-btn.next {
    right: 10px;
  }

  .carousel-dots {
    bottom: 20px;
    gap: 10px;
    padding: 10px 16px;
  }

  .dot {
    width: 8px;
    height: 8px;
  }

  .dot.active {
    width: 28px;
  }

  .image-wrapper {
    max-height: 70vh;
  }
}
</style>
