<template>
  <transition name="modal-fade">
    <div v-if="isOpen" class="modal-overlay" @click.self="closeModal">
      <div class="modal-content">
        <button class="modal-close" @click="closeModal" aria-label="Close modal">
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
            <line x1="18" y1="6" x2="6" y2="18"></line>
            <line x1="6" y1="6" x2="18" y2="18"></line>
          </svg>
        </button>

        <div class="modal-body">
          <div class="modal-image">
            <img :src="product.image" :alt="product.name" :class="product.imageClass" />
          </div>

          <div class="modal-details">
            <h2>{{ product.name }}</h2>

            <div class="product-price">
              <span class="label">Price:</span>
              <span class="value">{{ product.srp }}</span>
            </div>

            <div class="product-materials">
              <span class="label">Materials:</span>
              <ul>
                <li v-for="(material, index) in product.materials" :key="index">
                  {{ material }}
                </li>
              </ul>
            </div>

            <div class="product-difficulty">
              <span class="label">Difficulty Level:</span>
              <div class="difficulty-stars">
                <span
                  v-for="n in 5"
                  :key="n"
                  :class="['star', { filled: n <= product.difficulty }]"
                >
                  ★
                </span>
              </div>
            </div>

            <div class="product-description">
              <span class="label">Description:</span>
              <p v-html="product.description"></p>
            </div>

            <div class="product-pattern">
              <span class="label">Crochet Pattern:</span>
              <p class="pattern-text" v-html="product.pattern"></p>
            </div>

            <button class="order-btn" @click="handleOrder">
              <span>Get This Item</span>
              <span class="icon">→</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps({
  product: {
    type: Object,
    required: true,
  },
  isOpen: {
    type: Boolean,
    required: true,
  },
})

const emit = defineEmits(['close', 'order'])

const closeModal = () => {
  emit('close')
}

const handleOrder = () => {
  emit('order')
  // Could redirect to contact or WhatsApp
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  padding: 1rem;
  overflow-y: auto;
}

.modal-content {
  background: #ffffff;
  border-radius: 24px;
  max-width: 900px;
  width: 100%;
  position: relative;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
  max-height: 90vh;
  overflow-y: auto;
}

.modal-close {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  background: rgba(89, 13, 130, 0.1);
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: #590d82;
  transition: all 0.3s ease;
  z-index: 10;
}

.modal-close:hover {
  background: rgba(89, 13, 130, 0.2);
  transform: rotate(90deg);
}

.modal-body {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  padding: 2rem;
}

.modal-image {
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--color-cream);
  border-radius: 20px;
  min-height: 400px;
  padding: 2rem;
}

.modal-image img {
  max-width: 100%;
  max-height: 400px;
  object-fit: contain;
  display: block;
}

.modal-details {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.modal-details h2 {
  font-size: 2rem;
  color: #590d82;
  margin: 0;
}

.product-price,
.product-materials,
.product-difficulty,
.product-description,
.product-pattern {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.label {
  font-weight: 700;
  color: #590d82;
  font-size: 0.95rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.value {
  font-size: 1.5rem;
  font-weight: 700;
  color: #590d82;
}

.product-materials ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.product-materials li {
  background: rgba(89, 13, 130, 0.1);
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.9rem;
  color: #590d82;
}

.difficulty-stars {
  display: flex;
  gap: 0.5rem;
  font-size: 1.5rem;
}

.star {
  color: #ddd;
  transition: color 0.2s ease;
}

.star.filled {
  color: #ffd93d;
}

.product-description p,
.product-pattern p {
  margin: 0;
  line-height: 1.6;
  color: #333;
}

.pattern-text {
  background: rgba(89, 13, 130, 0.05);
  padding: 1rem;
  border-radius: 12px;
  border-left: 4px solid #590d82;
  font-family: 'Courier New', monospace;
  font-size: 0.9rem;
  max-height: 200px;
  overflow-y: auto;
}

.order-btn {
  background: linear-gradient(135deg, #590d82 0%, #8b4fb9 100%);
  color: #ffffff;
  border: none;
  border-radius: 12px;
  padding: 1rem 2rem;
  font-size: 1.05rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  margin-top: 1rem;
}

.order-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(89, 13, 130, 0.3);
}

.order-btn:active {
  transform: translateY(0);
}

.icon {
  font-size: 1.3rem;
  transition: transform 0.3s ease;
}

.order-btn:hover .icon {
  transform: translateX(4px);
}

/* Modal transitions */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: all 0.3s ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}

.modal-fade-enter-active .modal-content,
.modal-fade-leave-active .modal-content {
  transition: transform 0.3s ease;
}

.modal-fade-enter-from .modal-content,
.modal-fade-leave-to .modal-content {
  transform: scale(0.95);
}

/* Responsive */
@media (max-width: 768px) {
  .modal-body {
    grid-template-columns: 1fr;
    gap: 1.5rem;
    padding: 1.5rem;
  }

  .modal-close {
    top: 1rem;
    right: 1rem;
  }

  .modal-details h2 {
    font-size: 1.5rem;
  }

  .modal-image {
    min-height: 280px;
    order: -1;
  }

  .modal-image img {
    max-height: 280px;
  }
}
</style>
