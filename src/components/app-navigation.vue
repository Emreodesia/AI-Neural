<template>
  <nav class="navbar" :class="{ 'scrolled': isScrolled }">
    <div class="nav-container">
      <div class="nav-brand">
        <span class="brand-text">AI<span class="accent">Neural</span></span>
      </div>
      <div class="nav-menu" :class="{ 'active': mobileMenuOpen }">
        <a href="#home" class="nav-link" @click="scrollTo('home')">Home</a>
        <a href="#features" class="nav-link" @click="scrollTo('features')">Features</a>
        <a href="#testimonials" class="nav-link" @click="scrollTo('testimonials')">Testimonials</a>
        <a href="#pricing" class="nav-link" @click="scrollTo('pricing')">Pricing</a>
        <button class="cta-button" @click="openEarlyAccessModal">Get Early Access</button>
      </div>
      <div class="hamburger" @click="toggleMobileMenu">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
  </nav>
  
  <!-- Early Access Modal -->
  <AppEarlyAccessModal 
    :is-open="isEarlyAccessModalOpen" 
    @close="closeEarlyAccessModal" 
  />
</template>

<script setup>
import { ref } from 'vue'
import AppEarlyAccessModal from './app-early-access-modal.vue'

// Props
const props = defineProps({
  isScrolled: {
    type: Boolean,
    default: false
  }
})

// Emits
const emit = defineEmits(['scroll-to', 'toggle-mobile-menu'])

// Reactive data
const mobileMenuOpen = ref(false)
const isEarlyAccessModalOpen = ref(false)

// Methods
const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
  // Prevent body scroll when menu is open
  if (mobileMenuOpen.value) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = 'auto'
  }
  emit('toggle-mobile-menu', mobileMenuOpen.value)
}

const scrollTo = (elementId) => {
  const element = document.getElementById(elementId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
  mobileMenuOpen.value = false
  // Restore body scroll
  document.body.style.overflow = 'auto'
  emit('scroll-to', elementId)
}

const openEarlyAccessModal = () => {
  isEarlyAccessModalOpen.value = true
  mobileMenuOpen.value = false
  // Prevent body scroll when modal is open
  document.body.style.overflow = 'hidden'
}

const closeEarlyAccessModal = () => {
  isEarlyAccessModalOpen.value = false
  // Restore body scroll
  document.body.style.overflow = 'auto'
}
</script>

<style scoped>
/* Navigation */
.navbar {
  position: fixed;
  top: 0;
  margin-bottom: 10px;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(13, 13, 13, 0.3);
  backdrop-filter: blur(30px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.navbar.scrolled {
  background: rgba(13, 13, 13, 0.85);
  backdrop-filter: blur(40px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 8px 32px rgba(0, 255, 255, 0.15);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 2rem;
  width: 100%;
  box-sizing: border-box;
}

.brand-text {
  font-size: 1.5rem;
  font-weight: 700;
  color: #ffffff;
}

.accent {
  color: #00FFFF;
}

.nav-menu {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.nav-link {
  color: #ffffff;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
  cursor: pointer;
}

.nav-link:hover {
  color: #00FFFF;
}

.cta-button {
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  color: #ffffff;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
  box-shadow: 0 5px 20px rgba(0, 255, 255, 0.2);
}

.cta-button::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s;
}

.cta-button:hover::before {
  left: 100%;
}

.cta-button:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 15px 35px rgba(0, 255, 255, 0.4);
}

.hamburger {
  display: none;
  flex-direction: column;
  cursor: pointer;
  gap: 4px;
}

.hamburger span {
  width: 25px;
  height: 3px;
  background: #ffffff;
  transition: 0.3s;
}

/* Mobile Styles */
@media (max-width: 768px) {
  .hamburger {
    display: flex;
  }
  
  .nav-menu {
    position: fixed;
    top: 100%;
    left: 0;
    right: 0;
    background: rgba(13, 13, 13, 0.98);
    backdrop-filter: blur(20px);
    flex-direction: column;
    padding: 2rem;
    transition: all 0.3s ease;
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
  }
  
  .nav-menu.active {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }
  
  .nav-menu .nav-link {
    padding: 1rem 0;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    width: 100%;
    text-align: center;
  }
  
  .nav-menu .cta-button {
    margin-top: 1rem;
    width: 100%;
  }
}

@media (max-width: 480px) {
  .nav-container {
    padding: 1rem;
  }
}
</style> 