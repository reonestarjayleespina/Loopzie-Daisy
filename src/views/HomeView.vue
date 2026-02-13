<template>
  <section class="hero">
    <div class="hero-text">
      <p class="eyebrow">Playful blooms for everyday rituals</p>
      <h1>Fresh, bright, and made to loop you in.</h1>
      <p class="lede">
        Loopzie Daisy crafts cheerful floral moments with a modern twist. Explore seasonal bundles,
        curated gifts, and custom arrangements.
      </p>
      <div class="cta-row">
        <button class="primary-btn" type="button">Shop the Catalog</button>
        <button class="ghost-btn" type="button">Book a Custom Order</button>
      </div>
    </div>
    <div class="hero-card">
      <div class="card-title">Today’s Spotlight</div>
      <div class="card-body">
        <p class="card-label">Sunlit Daisy Box</p>
        <p class="card-note">Bright yellows, creamy whites, and lush greens.</p>
        <button class="primary-btn" type="button">Add to Cart</button>
      </div>
    </div>
  </section>

  <section class="highlights">
    <div class="highlight">
      <h2>Seasonal Collections</h2>
      <p>Limited drops every month with fresh stems and bold palettes.</p>
    </div>
    <div class="highlight">
      <h2>Same-Day Delivery</h2>
      <p>Order before noon to send a surprise bouquet across town.</p>
    </div>
    <div class="highlight">
      <h2>Custom Styling</h2>
      <p>Work with our designers for events, weddings, and brand shoots.</p>
    </div>
  </section>
</template>

<style scoped>
.hero {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 2rem;
  align-items: center;
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

.cta-row {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.ghost-btn {
  background: transparent;
  color: var(--color-purple);
  border: 2px solid var(--color-purple);
  border-radius: 999px;
  padding: 0.75rem 1.6rem;
  font-weight: 700;
  cursor: pointer;
  transition:
    transform 0.2s ease,
    box-shadow 0.2s ease;
}

.ghost-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(89, 13, 130, 0.15);
}

.hero-card {
  background: #ffffff;
  border-radius: 24px;
  border: 2px solid var(--color-purple);
  padding: 2rem;
  box-shadow: 0 16px 35px rgba(89, 13, 130, 0.16);
}

.card-title {
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.2em;
  font-size: 0.7rem;
  margin-bottom: 1rem;
}

.card-label {
  font-size: 1.4rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.card-note {
  margin-bottom: 1.5rem;
}

.highlights {
  margin-top: 3rem;
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
}

.highlight {
  background: #ffffff;
  border-radius: 18px;
  padding: 1.5rem;
  border: 1px solid rgba(89, 13, 130, 0.2);
}

.highlight h2 {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
}
</style>
