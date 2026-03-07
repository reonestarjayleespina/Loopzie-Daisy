<template>
  <div class="carousel-container">
    <div class="carousel-wrapper">
      <transition-group name="slide" tag="div" class="carousel-track">
        <div
          v-for="(image, index) in images"
          :key="image"
          v-show="index === currentIndex"
          class="carousel-slide"
        >
          <img :src="image" :alt="`Crochet product ${index + 1}`" />
        </div>
      </transition-group>

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
let autoplayInterval = null

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % images.length
}

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + images.length) % images.length
}

const goToSlide = (index) => {
  currentIndex.value = index
  // Reset autoplay timer when user manually navigates
  if (autoplayInterval) {
    clearInterval(autoplayInterval)
    startAutoplay()
  }
}

const startAutoplay = () => {
  autoplayInterval = setInterval(() => {
    nextSlide()
  }, 3000) // Change slide every 3 seconds
}

onMounted(() => {
  startAutoplay()
})

onUnmounted(() => {
  if (autoplayInterval) {
    clearInterval(autoplayInterval)
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
  background: var(--color-cream);
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

.carousel-slide img {
  max-width: 100%;
  max-height: 80vh;
  object-fit: contain;
  display: block;
  width: auto;
  height: auto;
}

/* Slide transitions */
.slide-enter-active,
.slide-leave-active {
  transition: all 0.6s ease-in-out;
}

.slide-enter-from {
  opacity: 0;
  transform: translateX(100%);
}

.slide-leave-to {
  opacity: 0;
  transform: translateX(-100%);
}

/* Navigation buttons */
.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.9);
  border: none;
  border-radius: 50%;
  width: 45px;
  height: 45px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
  color: #590d82;
  margin: 0;
}

.carousel-btn:hover {
  background: #ffffff;
  transform: translateY(-50%) scale(1.1);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
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
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 10px;
  z-index: 10;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: 2px solid #ffffff;
  background: rgba(255, 255, 255, 0.4);
  cursor: pointer;
  transition: all 0.3s ease;
  padding: 0;
}

.dot:hover {
  background: rgba(255, 255, 255, 0.7);
  transform: scale(1.2);
}

.dot.active {
  background: #ffffff;
  width: 30px;
  border-radius: 6px;
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
    width: 35px;
    height: 35px;
  }

  .carousel-btn.prev {
    left: 10px;
  }

  .carousel-btn.next {
    right: 10px;
  }

  .carousel-dots {
    bottom: 15px;
    gap: 8px;
  }

  .dot {
    width: 10px;
    height: 10px;
  }

  .dot.active {
    width: 24px;
  }
}
</style>
