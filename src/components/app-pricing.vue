<template>
  <section id="pricing" class="pricing">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Choose Your Plan</h2>
        <p class="section-subtitle">Flexible pricing designed to scale with your business needs</p>
      </div>
      <div class="pricing-grid">
        <div class="pricing-card" v-for="(plan, index) in pricingPlans" :key="plan.id" :class="{ 'featured': plan.featured }" :style="{ animationDelay: `${index * 0.2}s` }">
          <div class="card-header">
            <div class="plan-badge" v-if="plan.badge">{{ plan.badge }}</div>
            <h3>{{ plan.name }}</h3>
            <p class="plan-description">{{ plan.description }}</p>
          </div>
          <div class="pricing-section">
            <div class="price">
              <span class="currency">$</span>
              <span class="amount">{{ plan.price }}</span>
              <span class="period">/month</span>
            </div>
            <div class="price-note" v-if="plan.priceNote">{{ plan.priceNote }}</div>
          </div>
          <div class="features-section">
            <h4>What's included:</h4>
            <ul class="features-list">
              <li v-for="feature in plan.features" :key="feature" :class="{ 'highlight': feature.highlight }">
                <i class="check-icon">✓</i>
                <span>{{ feature.text }}</span>
                <span class="feature-badge" v-if="feature.badge">{{ feature.badge }}</span>
              </li>
            </ul>
          </div>
          <div class="card-footer">
            <button 
              class="pricing-cta" 
              :class="{ 'primary': plan.featured }"
              @click="handlePlanAction(plan)"
            >
              {{ plan.cta }}
            </button>
            <p class="trial-note" v-if="plan.trialNote">{{ plan.trialNote }}</p>
          </div>
        </div>
      </div>
      <div class="pricing-note">
        <p>All plans include 24/7 support, 99.9% uptime SLA, and enterprise-grade security.</p>
        <p>Need a custom plan? <a href="#contact">Contact our sales team</a></p>
      </div>
    </div>
    
    <!-- Early Access Modal -->
    <AppEarlyAccessModal 
      :is-open="isEarlyAccessModalOpen" 
      @close="closeEarlyAccessModal" 
    />
  </section>
</template>

<script setup>
import { ref } from 'vue'
import AppEarlyAccessModal from './app-early-access-modal.vue'

// Reactive data
const isEarlyAccessModalOpen = ref(false)

// Pricing data
const pricingPlans = ref([
  {
    id: 1,
    name: 'Starter',
    description: 'Perfect for small teams and startups',
    price: 0,
    priceNote: 'Free forever',
    badge: 'Free',
    features: [
      { text: 'Basic API Access', highlight: false },
      { text: '1,000 requests/month', highlight: false },
      { text: 'Community Support', highlight: false },
      { text: 'Basic Analytics Dashboard', highlight: false },
      { text: 'Standard Integrations', highlight: false }
    ],
    cta: 'Get Started Free',
    trialNote: 'No credit card required',
    featured: false,
    action: 'early-access'
  },
  {
    id: 2,
    name: 'Professional',
    description: 'Ideal for growing businesses',
    price: 99,
    priceNote: 'Most popular',
    badge: 'Popular',
    features: [
      { text: 'Advanced API Access', highlight: true },
      { text: '50,000 requests/month', highlight: false },
      { text: 'Priority Support', highlight: true },
      { text: 'Advanced Analytics & Reports', highlight: true },
      { text: 'Custom Integrations', highlight: true },
      { text: 'White-label Solutions', highlight: false },
      { text: 'Dedicated Account Manager', highlight: false }
    ],
    cta: 'Start Building',
    trialNote: '14-day free trial',
    featured: true,
    action: 'early-access'
  },
  {
    id: 3,
    name: 'Enterprise',
    description: 'For large-scale operations',
    price: 299,
    priceNote: 'Custom pricing available',
    badge: 'Enterprise',
    features: [
      { text: 'Enterprise API Access', highlight: true },
      { text: 'Unlimited requests', highlight: true, badge: 'Unlimited' },
      { text: '24/7 Premium Support', highlight: true },
      { text: 'Real-time Analytics & AI Insights', highlight: true },
      { text: 'Custom AI Model Training', highlight: true },
      { text: 'White-label Solutions', highlight: true },
      { text: 'Dedicated Account Manager', highlight: true },
      { text: 'SLA Guarantee', highlight: true, badge: '99.9%' }
    ],
    cta: 'Contact Sales',
    trialNote: 'Custom demo available',
    featured: false,
    action: 'contact-sales'
  }
])

// Methods
const handlePlanAction = (plan) => {
  if (plan.action === 'early-access') {
    openEarlyAccessModal()
  } else if (plan.action === 'contact-sales') {
    // Handle contact sales action
    console.log('Contact sales for:', plan.name)
    // You could open a different modal or redirect to contact page
  }
}

const openEarlyAccessModal = () => {
  isEarlyAccessModalOpen.value = true
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
/* Sections */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  width: 100%;
  box-sizing: border-box;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title {
  font-size: clamp(2.5rem, 5vw, 3.5rem);
  font-weight: 800;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #ffffff 0%, #00FFFF 50%, #9A00FF 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  background-size: 200% 200%;
  animation: gradientShift 3s ease-in-out infinite;
}

.section-subtitle {
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.8);
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.6;
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

/* Pricing Section */
.pricing {
  padding: 8rem 0;
  background: linear-gradient(180deg, rgba(26, 26, 46, 0.3) 0%, rgba(22, 33, 62, 0.1) 100%);
  position: relative;
  overflow: hidden;
}

.pricing::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 20%, rgba(0, 255, 255, 0.05) 0%, transparent 50%),
    radial-gradient(circle at 80% 80%, rgba(154, 0, 255, 0.05) 0%, transparent 50%);
  pointer-events: none;
}

.pricing-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2.5rem;
  max-width: 1100px;
  margin: 0 auto;
  width: 100%;
  position: relative;
  z-index: 1;
  margin-bottom: 4rem;
}

.pricing-card {
  background: rgba(31, 31, 31, 0.4);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 24px;
  padding: 2.5rem;
  text-align: left;
  position: relative;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  width: 100%;
  box-sizing: border-box;
  min-height: 500px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  overflow: hidden;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s ease-out forwards;
}

.pricing-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(0, 255, 255, 0.05), rgba(154, 0, 255, 0.05));
  opacity: 0;
  transition: opacity 0.3s ease;
}

.pricing-card:hover::before {
  opacity: 1;
}

.pricing-card.featured {
  border-color: #00FFFF;
  transform: scale(1.05);
  box-shadow: 
    0 25px 80px rgba(0, 255, 255, 0.2),
    0 0 0 1px rgba(0, 255, 255, 0.1);
}

.pricing-card.featured::after {
  content: 'Most Popular';
  position: absolute;
  top: 20px;
  right: -30px;
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  color: #ffffff;
  padding: 0.5rem 2rem;
  font-size: 0.8rem;
  font-weight: 600;
  transform: rotate(45deg);
  box-shadow: 0 5px 15px rgba(0, 255, 255, 0.3);
}

.pricing-card:hover {
  transform: translateY(-10px) scale(1.02);
  border-color: rgba(0, 255, 255, 0.3);
  box-shadow: 
    0 25px 80px rgba(0, 255, 255, 0.15),
    0 0 0 1px rgba(0, 255, 255, 0.1);
}

.pricing-card.featured:hover {
  transform: translateY(-10px) scale(1.07);
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.card-header {
  margin-bottom: 2rem;
}

.plan-badge {
  display: inline-block;
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  color: #ffffff;
  padding: 0.4rem 1rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  margin-bottom: 1rem;
  box-shadow: 0 5px 15px rgba(0, 255, 255, 0.3);
}

.pricing-card h3 {
  font-size: 1.8rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: #ffffff;
}

.plan-description {
  color: rgba(255, 255, 255, 0.7);
  font-size: 1rem;
  line-height: 1.5;
}

.pricing-section {
  margin-bottom: 2rem;
  text-align: center;
}

.price {
  display: flex;
  align-items: baseline;
  justify-content: center;
  margin-bottom: 0.5rem;
}

.currency {
  font-size: 1.5rem;
  color: rgba(255, 255, 255, 0.7);
  font-weight: 600;
}

.amount {
  font-size: 3.5rem;
  font-weight: 800;
  color: #00FFFF;
  text-shadow: 0 0 20px rgba(0, 255, 255, 0.3);
  margin: 0 0.2rem;
}

.period {
  color: rgba(255, 255, 255, 0.7);
  font-size: 1.1rem;
  font-weight: 500;
}

.price-note {
  color: #9A00FF;
  font-size: 0.9rem;
  font-weight: 600;
  text-align: center;
}

.features-section {
  margin-bottom: 2rem;
  flex-grow: 1;
}

.features-section h4 {
  font-size: 1.1rem;
  font-weight: 600;
  color: #ffffff;
  margin-bottom: 1rem;
}

.features-list {
  list-style: none;
  margin: 0;
  padding: 0;
}

.features-list li {
  padding: 0.8rem 0;
  display: flex;
  align-items: center;
  gap: 0.8rem;
  color: rgba(255, 255, 255, 0.8);
  font-size: 0.95rem;
  line-height: 1.4;
}

.features-list li.highlight {
  color: #ffffff;
  font-weight: 500;
}

.check-icon {
  color: #00FFFF;
  font-weight: bold;
  font-size: 1.1rem;
  min-width: 20px;
  text-align: center;
}

.feature-badge {
  background: rgba(0, 255, 255, 0.2);
  color: #00FFFF;
  padding: 0.2rem 0.5rem;
  border-radius: 10px;
  font-size: 0.7rem;
  font-weight: 600;
  margin-left: auto;
}

.card-footer {
  text-align: center;
}

.pricing-cta {
  width: 100%;
  background: rgba(255, 255, 255, 0.1);
  color: #ffffff;
  border: 2px solid rgba(255, 255, 255, 0.2);
  padding: 1.2rem;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-bottom: 1rem;
}

.pricing-cta.primary {
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  border-color: transparent;
  box-shadow: 0 10px 30px rgba(0, 255, 255, 0.3);
}

.pricing-cta:hover {
  transform: translateY(-2px);
  border-color: #00FFFF;
  box-shadow: 0 15px 40px rgba(0, 255, 255, 0.2);
}

.pricing-cta.primary:hover {
  box-shadow: 0 20px 50px rgba(0, 255, 255, 0.4);
}

.trial-note {
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.85rem;
  margin: 0;
}

.pricing-note {
  text-align: center;
  color: rgba(255, 255, 255, 0.7);
  font-size: 1rem;
  line-height: 1.6;
  position: relative;
  z-index: 1;
}

.pricing-note a {
  color: #00FFFF;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s ease;
}

.pricing-note a:hover {
  color: #9A00FF;
}

/* Responsive Design */
@media (max-width: 1024px) {
  .container {
    padding: 0 1.5rem;
  }
  
  .pricing-grid {
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 2rem;
  }
  
  .pricing-card {
    padding: 2rem;
    min-height: 480px;
  }
}

@media (max-width: 768px) {
  .pricing {
    padding: 6rem 0;
  }
  
  .pricing-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .pricing-card {
    padding: 2rem;
    min-height: 450px;
  }
  
  .section-title {
    font-size: clamp(2rem, 6vw, 3rem);
    margin-bottom: 1rem;
    padding: 0 1rem;
  }
  
  .section-subtitle {
    font-size: 1.1rem;
    padding: 0 1rem;
  }
  
  .amount {
    font-size: 3rem;
  }
  
  .pricing-card h3 {
    font-size: 1.6rem;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 1rem;
  }
  
  .pricing-card {
    padding: 1.5rem;
    min-height: 420px;
  }
  
  .pricing-card h3 {
    font-size: 1.4rem;
  }
  
  .amount {
    font-size: 2.5rem;
  }
  
  .section-title {
    font-size: clamp(1.8rem, 7vw, 2.5rem);
    padding: 0 0.5rem;
  }
  
  .section-subtitle {
    font-size: 1rem;
    padding: 0 0.5rem;
  }
  
  .features-list li {
    font-size: 0.9rem;
    padding: 0.6rem 0;
  }
}
</style> 