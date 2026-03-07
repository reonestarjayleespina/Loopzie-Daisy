<template>
  <section class="catalog">
    <CarouselSlider />

    <div class="catalog-header">
      <h1>Catalog</h1>
      <p>Discover seasonal bouquets, gift bundles, and curated arrangements.</p>
    </div>
    <div class="catalog-grid">
      <article class="catalog-card">
        <h2>Sunlit Daisy Box</h2>
        <p>Cheerful yellows and creamy whites for instant warmth.</p>
        <button class="primary-btn" type="button">View Details</button>
      </article>
      <article class="catalog-card">
        <h2>Lavender Drift</h2>
        <p>Soft purple blooms with a hint of citrus greens.</p>
        <button class="primary-btn" type="button">View Details</button>
      </article>
      <article class="catalog-card">
        <h2>Garden Party</h2>
        <p>Playful mix of wildflowers, perfect for celebrations.</p>
        <button class="primary-btn" type="button">View Details</button>
      </article>
    </div>
  </section>
</template>

<script setup>
import CarouselSlider from '@/components/CarouselSlider.vue'
</script>

<style scoped>
.catalog-header h1 {
  font-size: clamp(2rem, 3vw, 2.6rem);
  margin-bottom: 0.75rem;
}

.catalog-grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  margin-top: 2rem;
}

.catalog-card {
  background: #ffffff;
  border-radius: 18px;
  padding: 1.5rem;
  border: 2px solid rgba(89, 13, 130, 0.2);
  display: grid;
  gap: 1rem;
}
</style>
