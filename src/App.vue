
<template>
  <div id="app">
    <!-- Sticky Navigation -->
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
          <button class="cta-button">Get Early Access</button>
        </div>
        <div class="hamburger" @click="toggleMobileMenu">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
      <div class="hero-background">
        <div class="neural-network">
          <div class="node" v-for="i in 20" :key="i" :style="getNodeStyle(i)"></div>
          <svg class="connections">
            <line v-for="line in connections" :key="line.id" 
                  :x1="line.x1" :y1="line.y1" :x2="line.x2" :y2="line.y2" 
                  class="connection-line"/>
          </svg>
        </div>
      </div>
      <div class="hero-content">
        <h1 class="hero-title">
          Empower your business with AI
          <span class="gradient-text">Real-time intelligence, built for scale</span>
        </h1>
        <p class="hero-subtitle">
          We are an AI-first company building scalable, ethical, and efficient machine intelligence tools.
        </p>
        <div class="hero-buttons">
          <button class="cta-primary">Try Our AI Now</button>
          <button class="cta-secondary">Book a Demo</button>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="features">
      <div class="container">
        <h2 class="section-title">AI-Powered Features</h2>
        <div class="features-grid">
          <div class="feature-card" v-for="feature in features" :key="feature.id">
            <div class="feature-icon">
              <i :class="feature.icon"></i>
            </div>
            <h3>{{ feature.title }}</h3>
            <p>{{ feature.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials Section -->
    <section id="testimonials" class="testimonials">
      <div class="container">
        <h2 class="section-title">What Our Clients Say</h2>
        <div class="testimonials-grid">
          <div class="testimonial-card" v-for="testimonial in testimonials" :key="testimonial.id">
            <div class="testimonial-content">
              <p>"{{ testimonial.content }}"</p>
            </div>
            <div class="testimonial-author">
              <img :src="testimonial.avatar" :alt="testimonial.name" class="avatar">
              <div class="author-info">
                <h4>{{ testimonial.name }}</h4>
                <span>{{ testimonial.position }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Pricing Section -->
    <section id="pricing" class="pricing">
      <div class="container">
        <h2 class="section-title">Choose Your Plan</h2>
        <div class="pricing-grid">
          <div class="pricing-card" v-for="plan in pricingPlans" :key="plan.id" :class="{ 'featured': plan.featured }">
            <div class="pricing-header">
              <h3>{{ plan.name }}</h3>
              <div class="price">
                <span class="currency">$</span>
                <span class="amount">{{ plan.price }}</span>
                <span class="period">/month</span>
              </div>
            </div>
            <ul class="features-list">
              <li v-for="feature in plan.features" :key="feature">
                <i class="check-icon">✓</i>
                {{ feature }}
              </li>
            </ul>
            <button class="pricing-cta" :class="{ 'primary': plan.featured }">
              {{ plan.cta }}
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-brand">
            <span class="brand-text">AI<span class="accent">Neural</span></span>
            <p>Building the future of AI-powered solutions</p>
          </div>
          <div class="footer-links">
            <div class="link-group">
              <h4>Product</h4>
              <a href="#">Features</a>
              <a href="#">API Docs</a>
              <a href="#">Integrations</a>
            </div>
            <div class="link-group">
              <h4>Company</h4>
              <a href="#">About</a>
              <a href="#">Careers</a>
              <a href="#">Contact</a>
            </div>
          </div>
        </div>
        <div class="footer-bottom">
          <p>&copy; 2024 AINeural. All rights reserved.</p>
        </div>
      </div>
    </footer>

    <!-- Mobile CTA -->
    <div class="mobile-cta" v-show="showMobileCTA">
      <button class="mobile-cta-button">Start Building</button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Reactive data
const isScrolled = ref(false)
const mobileMenuOpen = ref(false)
const showMobileCTA = ref(false)
const connections = ref([])

// Features data
const features = ref([
  {
    id: 1,
    icon: '🧠',
    title: 'Natural Language API',
    description: 'Advanced NLP processing with real-time understanding and contextual responses.'
  },
  {
    id: 2,
    icon: '⚡',
    title: 'Real-time Analytics',
    description: 'Get instant insights with our lightning-fast data processing engine.'
  },
  {
    id: 3,
    icon: '🔧',
    title: 'Smart Automation Engine',
    description: 'Automate complex workflows with intelligent decision-making capabilities.'
  },
  {
    id: 4,
    icon: '🔗',
    title: 'Seamless Integrations',
    description: 'Connect with your favorite tools and platforms with our robust API.'
  }
])

// Testimonials data
const testimonials = ref([
  {
    id: 1,
    content: 'AINeural transformed our business operations. The real-time insights are game-changing.',
    name: 'Sarah Chen',
    position: 'CTO, TechCorp',
    avatar: 'https://images.unsplash.com/photo-1494790108755-2616b612b786?w=64&h=64&fit=crop&crop=face'
  },
  {
    id: 2,
    content: 'The API integration was seamless. Our development team was up and running in hours.',
    name: 'Michael Rodriguez',
    position: 'Lead Developer, Innovate Labs',
    avatar: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=64&h=64&fit=crop&crop=face'
  },
  {
    id: 3,
    content: 'Outstanding AI capabilities. The automation engine saved us countless hours.',
    name: 'Emily Johnson',
    position: 'Product Manager, FutureAI',
    avatar: 'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=64&h=64&fit=crop&crop=face'
  }
])

// Pricing data
const pricingPlans = ref([
  {
    id: 1,
    name: 'Free',
    price: 0,
    features: ['Basic API Access', '1,000 requests/month', 'Community Support', 'Basic Analytics'],
    cta: 'Try Free',
    featured: false
  },
  {
    id: 2,
    name: 'Startup',
    price: 99,
    features: ['Advanced API Access', '50,000 requests/month', 'Priority Support', 'Advanced Analytics', 'Custom Integrations'],
    cta: 'Start Building',
    featured: true
  },
  {
    id: 3,
    name: 'Scale',
    price: 299,
    features: ['Enterprise API Access', 'Unlimited requests', '24/7 Support', 'Real-time Analytics', 'White-label Solutions', 'Dedicated Account Manager'],
    cta: 'Contact Sales',
    featured: false
  }
])

// Methods
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
  showMobileCTA.value = window.scrollY > window.innerHeight
}

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const scrollTo = (elementId) => {
  const element = document.getElementById(elementId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
  mobileMenuOpen.value = false
}

const getNodeStyle = (index) => {
  const angle = (index * 360 / 20) * (Math.PI / 180)
  const radius = 150 + Math.random() * 100
  const x = Math.cos(angle) * radius + 50
  const y = Math.sin(angle) * radius + 50
  
  return {
    left: `${x}%`,
    top: `${y}%`,
    animationDelay: `${index * 0.1}s`
  }
}

const generateConnections = () => {
  const nodes = []
  for (let i = 0; i < 20; i++) {
    const angle = (i * 360 / 20) * (Math.PI / 180)
    const radius = 150 + Math.random() * 100
    const x = (Math.cos(angle) * radius + 50) * window.innerWidth / 100
    const y = (Math.sin(angle) * radius + 50) * window.innerHeight / 100
    nodes.push({ x, y })
  }
  
  const newConnections = []
  for (let i = 0; i < nodes.length; i++) {
    for (let j = i + 1; j < nodes.length; j++) {
      if (Math.random() > 0.7) {
        newConnections.push({
          id: `${i}-${j}`,
          x1: nodes[i].x,
          y1: nodes[i].y,
          x2: nodes[j].x,
          y2: nodes[j].y
        })
      }
    }
  }
  connections.value = newConnections
}

// Lifecycle
onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  generateConnections()
  
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

/* Navigation */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(13, 13, 13, 0.8);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;
}

.navbar.scrolled {
  background: rgba(13, 13, 13, 0.95);
  box-shadow: 0 8px 32px rgba(0, 255, 255, 0.1);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 2rem;
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
  transition: all 0.3s ease;
}

.cta-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(0, 255, 255, 0.3);
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

/* Hero Section */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: radial-gradient(circle at 50% 50%, rgba(0, 255, 255, 0.1) 0%, transparent 50%);
}

.neural-network {
  position: relative;
  width: 100%;
  height: 100%;
}

.node {
  position: absolute;
  width: 8px;
  height: 8px;
  background: #00FFFF;
  border-radius: 50%;
  box-shadow: 0 0 20px #00FFFF;
  animation: pulse 2s infinite ease-in-out;
}

.connections {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.connection-line {
  stroke: rgba(0, 255, 255, 0.3);
  stroke-width: 1;
  animation: glow 3s infinite ease-in-out;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.5; transform: scale(1.2); }
}

@keyframes glow {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 0.8; }
}

.hero-content {
  position: relative;
  z-index: 10;
  text-align: center;
  max-width: 800px;
  padding: 0 2rem;
}

.hero-title {
  font-size: clamp(2.5rem, 5vw, 4rem);
  font-weight: 700;
  line-height: 1.2;
  margin-bottom: 1.5rem;
}

.gradient-text {
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  display: block;
  margin-top: 0.5rem;
}

.hero-subtitle {
  font-size: 1.25rem;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 2rem;
  line-height: 1.6;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.cta-primary {
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  color: #ffffff;
  border: none;
  padding: 1rem 2rem;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.cta-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(0, 255, 255, 0.4);
}

.cta-secondary {
  background: rgba(31, 31, 31, 0.8);
  color: #ffffff;
  border: 2px solid rgba(255, 255, 255, 0.2);
  padding: 1rem 2rem;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.cta-secondary:hover {
  border-color: #00FFFF;
  background: rgba(0, 255, 255, 0.1);
  transform: translateY(-3px);
}

/* Sections */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 700;
  text-align: center;
  margin-bottom: 3rem;
  background: linear-gradient(135deg, #ffffff, #00FFFF);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Features Section */
.features {
  padding: 6rem 0;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease;
}

.features.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.feature-card {
  background: rgba(31, 31, 31, 0.5);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  text-align: center;
  transition: all 0.3s ease;
  cursor: pointer;
}

.feature-card:hover {
  transform: translateY(-10px);
  border-color: rgba(0, 255, 255, 0.5);
  box-shadow: 0 20px 60px rgba(0, 255, 255, 0.1);
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.feature-card h3 {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: #ffffff;
}

.feature-card p {
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.6;
}

/* Testimonials Section */
.testimonials {
  padding: 6rem 0;
  background: rgba(31, 31, 31, 0.3);
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease;
}

.testimonials.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.testimonials-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
}

.testimonial-card {
  background: rgba(31, 31, 31, 0.8);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  transition: all 0.3s ease;
}

.testimonial-card:hover {
  transform: translateY(-5px);
  border-color: rgba(154, 0, 255, 0.5);
}

.testimonial-content {
  margin-bottom: 1.5rem;
}

.testimonial-content p {
  font-style: italic;
  color: rgba(255, 255, 255, 0.9);
  line-height: 1.6;
}

.testimonial-author {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  object-fit: cover;
}

.author-info h4 {
  font-weight: 600;
  color: #ffffff;
}

.author-info span {
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.9rem;
}

/* Pricing Section */
.pricing {
  padding: 6rem 0;
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease;
}

.pricing.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.pricing-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  max-width: 900px;
  margin: 0 auto;
}

.pricing-card {
  background: rgba(31, 31, 31, 0.5);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  text-align: center;
  position: relative;
  transition: all 0.3s ease;
}

.pricing-card.featured {
  border-color: #00FFFF;
  transform: scale(1.05);
  box-shadow: 0 20px 60px rgba(0, 255, 255, 0.2);
}

.pricing-card.featured::before {
  content: 'Most Popular';
  position: absolute;
  top: -10px;
  left: 50%;
  transform: translateX(-50%);
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  color: #ffffff;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
}

.pricing-header h3 {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.price {
  display: flex;
  align-items: baseline;
  justify-content: center;
  margin-bottom: 2rem;
}

.currency {
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.7);
}

.amount {
  font-size: 3rem;
  font-weight: 700;
  color: #00FFFF;
}

.period {
  color: rgba(255, 255, 255, 0.7);
}

.features-list {
  list-style: none;
  margin-bottom: 2rem;
}

.features-list li {
  padding: 0.5rem 0;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.check-icon {
  color: #00FFFF;
  font-weight: bold;
}

.pricing-cta {
  width: 100%;
  background: rgba(255, 255, 255, 0.1);
  color: #ffffff;
  border: 2px solid rgba(255, 255, 255, 0.2);
  padding: 1rem;
  border-radius: 50px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.pricing-cta.primary {
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  border-color: transparent;
}

.pricing-cta:hover {
  transform: translateY(-2px);
  border-color: #00FFFF;
}

/* Footer */
.footer {
  background: rgba(31, 31, 31, 0.8);
  backdrop-filter: blur(20px);
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding: 3rem 0 1rem;
}

.footer-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  margin-bottom: 2rem;
}

.footer-brand p {
  color: rgba(255, 255, 255, 0.7);
  margin-top: 0.5rem;
}

.footer-links {
  display: flex;
  gap: 3rem;
}

.link-group h4 {
  margin-bottom: 1rem;
  color: #00FFFF;
}

.link-group a {
  display: block;
  color: rgba(255, 255, 255, 0.7);
  text-decoration: none;
  margin-bottom: 0.5rem;
  transition: color 0.3s ease;
}

.link-group a:hover {
  color: #00FFFF;
}

.footer-bottom {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 1rem;
  text-align: center;
}

.footer-bottom p {
  color: rgba(255, 255, 255, 0.5);
}

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
    background: rgba(13, 13, 13, 0.95);
    backdrop-filter: blur(20px);
    flex-direction: column;
    padding: 2rem;
    transition: all 0.3s ease;
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
  }
  
  .nav-menu.active {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }
  
  .hero-buttons {
    flex-direction: column;
    align-items: center;
  }
  
  .cta-primary,
  .cta-secondary {
    width: 100%;
    max-width: 300px;
  }
  
  .features-grid,
  .testimonials-grid,
  .pricing-grid {
    grid-template-columns: 1fr;
  }
  
  .footer-content {
    grid-template-columns: 1fr;
    text-align: center;
  }
  
  .footer-links {
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .nav-container {
    padding: 1rem;
  }
  
  .hero-content {
    padding: 0 1rem;
  }
  
  .container {
    padding: 0 1rem;
  }
  
  .feature-card,
  .testimonial-card,
  .pricing-card {
    padding: 1.5rem;
  }
}
</style>
