<template>
  <div class="mobile-cta" v-show="show">
    <button class="mobile-cta-button">Start Building</button>
  </div>
</template>

<script setup>
// Props
defineProps({
  show: {
    type: Boolean,
    default: false
  }
})
</script>

<style scoped>
/* Mobile CTA */
.mobile-cta {
  position: fixed;
  bottom: 20px;
  right: 20px;
  z-index: 1000;
}

.mobile-cta-button {
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  color: #ffffff;
  border: none;
  padding: 1rem 1.5rem;
  border-radius: 50px;
  font-weight: 600;
  cursor: pointer;
  box-shadow: 0 10px 30px rgba(0, 255, 255, 0.3);
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
  40% { transform: translateY(-10px); }
  60% { transform: translateY(-5px); }
}

/* Responsive Design */
@media (max-width: 768px) {
  .mobile-cta {
    bottom: 15px;
    right: 15px;
  }
  
  .mobile-cta-button {
    padding: 0.8rem 1.2rem;
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .mobile-cta {
    bottom: 10px;
    right: 10px;
  }
  
  .mobile-cta-button {
    padding: 0.7rem 1rem;
    font-size: 0.85rem;
  }
}
</style> 