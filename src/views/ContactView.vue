<template>
  <section class="contact">
    <div class="contact-card">
      <h1>Contact</h1>
      <p>Tell us about your event, gift, or weekly floral needs.</p>
      <div class="contact-details">
        <p><strong>Email:</strong> hello@loopziedaisy.com</p>
        <p><strong>Phone:</strong> (555) 019-2202</p>
        <p><strong>Studio:</strong> 214 Bloom Lane, Aurora City</p>
      </div>
      <button class="primary-btn" type="button">Start a Custom Order</button>
    </div>
  </section>
</template>

<style scoped>
.contact {
  display: grid;
  place-items: center;
}

.contact-card {
  background: #ffffff;
  border-radius: 22px;
  padding: 2rem;
  border: 2px solid rgba(89, 13, 130, 0.2);
  max-width: 520px;
  display: grid;
  gap: 1rem;
}

.contact-details {
  display: grid;
  gap: 0.5rem;
}
</style>
