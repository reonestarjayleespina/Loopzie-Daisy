<script setup>
import { ref } from 'vue'
import CarouselSlider from './components/CarouselSlider.vue'
import ProductModal from './components/ProductModal.vue'
import tulipImage from './assets/crochet tulip.jpg'
import sunflowerImage from './assets/crochet sunflower.jpg'
import daisyImage from './assets/crochet daisy.jpg'
import roseImage from './assets/crochet rose.jpg'
import logoImage from './assets/LOOPZIE DAISY LOGO.png'

const selectedProduct = ref(null)
const showModal = ref(false)

const products = ref([
  {
    id: 1,
    name: 'Tulip 🌷',
    srp: '₱200',
    difficulty: 2,
    description:
      '<strong>Origin:</strong> Central Asia and Turkey (later made famous by the Netherlands).<br><br><strong>Colors:</strong> Almost every color imaginable, including soft pinks, bright yellows, deep purples, and rich reds.<br><br><strong>Description:</strong> A classic spring bloom symbolizing perfect and deep love. Their elegant, cup-shaped petals bring a sleek and modern feel to any floral arrangement.',
    materials: ['Acrylic Yarn', 'Crochet Hook (4.5mm)', 'Fiberfill', 'Stitch Marker'],
    pattern:
      '1 row - mc 6sc (6sc)<br>2 row - 2 sc each (12sc)<br>3 row - 1 sc 1 in (18sc)<br>4 row - 1 in 1sc 1sc (24)<br>5 row - sc each (24)<br>6 row - 1sc 1sc 1sc 1in (30)<br>7-12 - 1sc each',
    image: tulipImage,
    imageClass: 'img-tulip',
    showPattern: false,
  },
  {
    id: 2,
    name: 'Sunflower 🌻',
    srp: '₱250',
    difficulty: 3,
    description:
      '<strong>Origin:</strong> North and Central America.<br><br><strong>Colors:</strong> Traditionally bright golden-yellow petals with a rich, dark brown center.<br><br><strong>Description:</strong> Known for literally turning their heads to follow the sun, these bold and cheerful blooms represent pure happiness, loyalty, and adoration.',
    materials: ['Yellow Acrylic Yarn', 'Brown Acrylic Yarn', 'Crochet Hook (4.5mm)', 'Fiberfill'],
    pattern:
      '<strong>SUNFLOWER CENTER (Make 2)</strong><br>1 row - mc 6sc (6sc)<br>2 row - 2 sc each (12sc)<br>3 row - 1sc 1in (18sc)<br>4 row - 1sc 1sc 1in (24)<br>5 row - 1sc 1sc 1sc 1in (30)<br>6 row - 1sc 1sc 1sc 1sc 1in (36)<br><br><strong>PETALS</strong><br>sequence - ch2, (1dc 1tr) in 1st, ch3 picot, (1tr 1dc) in 1st, ch2, sl st in 1st',
    image: sunflowerImage,
    imageClass: 'img-sunflower',
    showPattern: false,
  },
  {
    id: 3,
    name: 'Daisy 🌼',
    srp: '₱150',
    difficulty: 1,
    description:
      '<strong>Origin:</strong> Europe and temperate regions of Asia.<br><br><strong>Colors:</strong> Iconic pristine white petals surrounding a sunny yellow center.<br><br><strong>Description:</strong> The namesake of our shop! Daisies are timeless, playful, and incredibly charming. They are the ultimate symbol of innocence, purity, and cheerful new beginnings.',
    materials: ['White Yarn', 'Yellow Yarn', 'Crochet Hook (4.5mm)', 'Fiberfill'],
    pattern: 'Center: Yellow 6sc. Petals: White ch 6, dc, hdc, sc.',
    image: daisyImage,
    imageClass: 'img-daisy',
    showPattern: false,
  },
  {
    id: 4,
    name: 'Rose 🌹',
    srp: '₱300',
    difficulty: 4,
    description:
      '<strong>Origin:</strong> Primarily Asia, with some species native to North America and Europe.<br><br><strong>Colors:</strong> Famous for deep romantic reds, but also beautifully bloom in pink, white, yellow, and orange.<br><br><strong>Description:</strong> The universal symbol of romance and passion. With their tightly layered, intricate petals, roses bring a touch of timeless elegance and luxury to any bouquet.',
    materials: ['Red/Pink Yarn', 'Green Yarn', 'Crochet Hook (4.5mm)', 'Fiberfill', 'Floral Wire'],
    pattern: 'Base: Chain 50. DC row. Scallop row. Roll tightly.',
    image: roseImage,
    imageClass: 'img-rose',
    showPattern: false,
  },
])

const togglePattern = (product) => {
  product.showPattern = !product.showPattern
}

const openModal = (product) => {
  selectedProduct.value = product
  showModal.value = true
}

const closeModal = () => {
  showModal.value = false
  selectedProduct.value = null
}

const handleOrder = () => {
  // Could integrate with WhatsApp, email form, or other contact method
  const productName = encodeURIComponent(selectedProduct.value.name)
  window.open(`https://www.facebook.com/loopsziedaisy`, '_blank')
  closeModal()
}
</script>

<template>
  <div class="app-shell">
    <header class="site-header">
      <h1 class="brand">Loopzie Daisy</h1>
      <img class="brand-logo" :src="logoImage" alt="Loopzie Daisy logo" />
    </header>

    <main class="site-main">
      <section class="catalog">
        <CarouselSlider />

        <div class="catalog-header">
          <h2>Crochet Product Catalog</h2>
          <p>Four signature blooms with patterns you can recreate at home.</p>
        </div>
        <div class="catalog-grid">
          <article
            v-for="product in products"
            :key="product.id"
            class="product-card"
            @click="openModal(product)"
          >
            <div class="product-image">
              <img :src="product.image" :alt="product.name" :class="product.imageClass" />
            </div>
            <div class="product-content">
              <h3>{{ product.name }}</h3>
              <p class="product-srp">SRP: {{ product.srp }}</p>
              <button class="primary-btn" type="button" @click.stop="togglePattern(product)">
                {{ product.showPattern ? 'Hide Pattern' : 'Show Pattern' }}
              </button>
              <p v-if="product.showPattern" class="product-pattern">{{ product.pattern }}</p>
            </div>
          </article>
        </div>
      </section>
    </main>

    <footer class="site-footer">
      <span>© 2026 Loopzie Daisy. All rights reserved.</span>
      <a
        class="footer-link"
        href="https://www.facebook.com/loopsziedaisy"
        target="_blank"
        rel="noopener"
      >
        Follow us on Facebook @loopsziedaisy
      </a>
    </footer>

    <ProductModal
      v-if="selectedProduct"
      :product="selectedProduct"
      :isOpen="showModal"
      @close="closeModal"
      @order="handleOrder"
    />
  </div>
</template>

<style scoped>
.app-shell {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  overflow-x: hidden;
}

.site-header {
  position: sticky;
  top: 0;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
  padding: 1rem 1.5rem;
  background: var(--color-purple);
  color: #ffffff;
  width: 100%;
}

.brand {
  font-weight: 700;
  font-size: 1.1rem;
  letter-spacing: 0.02em;
  margin: 0;
}

.brand-logo {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid var(--color-yellow);
  flex-shrink: 0;
}

.site-nav {
  display: flex;
  gap: 1.25rem;
  flex-wrap: wrap;
}

.site-nav a {
  color: #ffffff;
  font-weight: 600;
  transition: opacity 0.2s ease;
}

.site-nav a:hover {
  opacity: 0.8;
}

.site-main {
  flex: 1;
  padding: 0;
}

.site-footer {
  padding: 1.5rem;
  background: var(--color-purple);
  color: #ffffff;
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.footer-link {
  color: var(--color-yellow);
  font-weight: 600;
  text-decoration: underline;
}

.hero {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 2rem;
  align-items: center;
  margin-bottom: 3rem;
}

.hero-text h1 {
  font-size: clamp(2rem, 3.5vw, 3.2rem);
  line-height: 1.1;
  margin-bottom: 1rem;
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.2em;
  font-size: 0.75rem;
  font-weight: 700;
  margin-bottom: 0.75rem;
}

.lede {
  font-size: 1.05rem;
  max-width: 36rem;
  margin-bottom: 1.5rem;
}

.catalog-header {
  padding: 2.5rem 1.5rem 0;
}

.catalog-header h2 {
  font-size: clamp(1.6rem, 3vw, 2.4rem);
  margin-bottom: 0.5rem;
}

.catalog-grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  margin-top: 2rem;
  padding: 0 1.5rem 3rem;
}

.product-card {
  background: #ffffff;
  border-radius: 20px;
  border: 2px solid var(--color-purple);
  box-shadow: 0 14px 26px rgba(255, 217, 61, 0.35);
  overflow: hidden;
  display: grid;
  cursor: pointer;
  transition: all 0.3s ease;
}

.product-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 20px 40px rgba(89, 13, 130, 0.25);
  border-color: var(--color-yellow);
}

.product-image {
  height: 180px;
  overflow: hidden;
  background: #ffffff;
}

.product-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transform: scale(1);
}

.product-image img.img-tulip {
  transform: scale(1.1);
}

.product-image img.img-sunflower {
  object-position: center 40%;
}

.product-image img.img-daisy {
  object-position: center 45%;
}

.product-image img.img-rose {
  object-position: center 25%;
}

.product-content {
  padding: 1.5rem;
  display: grid;
  gap: 0.75rem;
}

.product-srp {
  font-weight: 600;
}

.product-pattern {
  font-size: 0.95rem;
  background: rgba(255, 217, 61, 0.25);
  padding: 0.75rem;
  border-radius: 12px;
}

@media (max-width: 720px) {
  .site-header {
    align-items: center;
  }

  .site-nav {
    gap: 0.75rem;
  }

  .site-main {
    padding: 2rem 1.25rem 2.5rem;
  }
}
</style>
