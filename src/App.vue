<template>
  <div id="app">
    <!-- Navigation Component -->
    <AppNavigation 
      :is-scrolled="isScrolled" 
      @scroll-to="scrollTo" 
      @toggle-mobile-menu="toggleMobileMenu" 
    />

    <!-- Hero Component -->
    <AppHero />

    <!-- Features Component -->
    <AppFeatures />

    <!-- Testimonials Component -->
    <AppTestimonials />

    <!-- Pricing Component -->
    <AppPricing />

    <!-- Footer Component -->
    <AppFooter />

    <!-- Mobile CTA Component -->
    <AppMobileCta :show="showMobileCTA" />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import AppNavigation from './components/app-navigation.vue'
import AppHero from './components/app-hero.vue'
import AppFeatures from './components/app-features.vue'
import AppTestimonials from './components/app-testimonials.vue'
import AppPricing from './components/app-pricing.vue'
import AppFooter from './components/app-footer.vue'
import AppMobileCta from './components/app-mobile-cta.vue'

// Reactive data
const isScrolled = ref(false)
const mobileMenuOpen = ref(false)
const showMobileCTA = ref(false)

// Methods
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
  showMobileCTA.value = window.scrollY > window.innerHeight
}

const toggleMobileMenu = (isOpen) => {
  mobileMenuOpen.value = isOpen
}

const scrollTo = (elementId) => {
  const element = document.getElementById(elementId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

// Lifecycle
onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  
  // Intersection Observer for animations
  const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px'
  }
  
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-in')
      }
    })
  }, observerOptions)
  
  // Observe all sections
  setTimeout(() => {
    document.querySelectorAll('.features, .testimonials, .pricing').forEach(el => {
      observer.observe(el)
    })
  }, 100)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: #0D0D0D;
  color: #ffffff;
  overflow-x: hidden;
}
</style> 