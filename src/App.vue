<script setup>
import { ref } from 'vue'
import tulipImage from './assets/crochet tulip.jpg'
import sunflowerImage from './assets/crochet sunflower.jpg'
import daisyImage from './assets/crochet daisy.jpg'
import roseImage from './assets/crochet rose.jpg'
import logoImage from './assets/LOOPZIE DAISY LOGO.png'

const products = ref([
  {
    id: 1,
    name: 'Tulip 🌷',
    srp: '₱200',
    pattern:
      'Round 1: sc 6x in the magic circle. Round 2: Inc in every sc. (12) Round 3: Inc, sc. (18) Round 4: Inc, sc 2x (24) Round 5: Inc, sc 3x (30) Round 6: Inc, sc 4x (36) Round 7: Inc, sc 5x (42) Round 8-15: Sc in every stitch. (42)',
    image: tulipImage,
    imageClass: 'img-tulip',
    showPattern: false,
  },
  {
    id: 2,
    name: 'Sunflower 🌻',
    srp: '₱250',
    pattern: 'Center: Brown 6sc in MR. Petals: Yellow ch 5, tr, ch 3, slst.',
    image: sunflowerImage,
    imageClass: 'img-sunflower',
    showPattern: false,
  },
  {
    id: 3,
    name: 'Daisy 🌼',
    srp: '₱150',
    pattern: 'Center: Yellow 6sc. Petals: White ch 6, dc, hdc, sc.',
    image: daisyImage,
    imageClass: 'img-daisy',
    showPattern: false,
  },
  {
    id: 4,
    name: 'Rose 🌹',
    srp: '₱300',
    pattern: 'Base: Chain 50. DC row. Scallop row. Roll tightly.',
    image: roseImage,
    imageClass: 'img-rose',
    showPattern: false,
  },
])

const togglePattern = (product) => {
  product.showPattern = !product.showPattern
}
</script>

<template>
  <div class="app-shell">
    <header class="site-header">
      <h1 class="brand">Loopzie Daisy</h1>
      <img class="brand-logo" :src="logoImage" alt="Loopzie Daisy logo" />
    </header>

    <main class="site-main">
      <section class="hero">
        <div class="hero-text">
          <h1>Handmade Blooms & Patterns</h1>
          <p class="lede">
            Discover crochet florals crafted with care, each paired with a pattern so you can make
            your own bouquet.
          </p>
        </div>
      </section>

      <section class="catalog">
        <div class="catalog-header">
          <h2>Crochet Product Catalog</h2>
          <p>Four signature blooms with patterns you can recreate at home.</p>
        </div>
        <div class="catalog-grid">
          <article v-for="product in products" :key="product.id" class="product-card">
            <div class="product-image">
              <img :src="product.image" :alt="product.name" :class="product.imageClass" />
            </div>
            <div class="product-content">
              <h3>{{ product.name }}</h3>
              <p class="product-srp">SRP: {{ product.srp }}</p>
              <button class="primary-btn" type="button" @click="togglePattern(product)">
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
  </div>
</template>

<style scoped>
.app-shell {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
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
  padding: 2.5rem 1.5rem 3rem;
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

.catalog-header h2 {
  font-size: clamp(1.6rem, 3vw, 2.4rem);
  margin-bottom: 0.5rem;
}

.catalog-grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  margin-top: 2rem;
}

.product-card {
  background: #ffffff;
  border-radius: 20px;
  border: 2px solid var(--color-purple);
  box-shadow: 0 14px 26px rgba(255, 217, 61, 0.35);
  overflow: hidden;
  display: grid;
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
