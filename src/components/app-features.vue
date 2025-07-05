<template>
  <section id="features" class="features">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">AI-Powered Features</h2>
        <p class="section-subtitle">Discover the cutting-edge capabilities that power the future of business intelligence</p>
      </div>
      <div class="features-grid">
        <div class="feature-card" v-for="(feature, index) in features" :key="feature.id" :style="{ animationDelay: `${index * 0.2}s` }">
          <div class="feature-icon-wrapper">
            <div class="feature-icon">
              <i :class="feature.icon"></i>
            </div>
            <div class="icon-glow"></div>
          </div>
          <h3>{{ feature.title }}</h3>
          <p>{{ feature.description }}</p>
          <div class="feature-link">
            <span>Learn More</span>
            <i class="arrow-icon">→</i>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// Features data
const features = ref([
  {
    id: 1,
    icon: '🧠',
    title: 'Natural Language API',
    description: 'Advanced NLP processing with real-time understanding and contextual responses that adapt to your business needs.'
  },
  {
    id: 2,
    icon: '⚡',
    title: 'Real-time Analytics',
    description: 'Get instant insights with our lightning-fast data processing engine that scales with your operations.'
  },
  {
    id: 3,
    icon: '🔧',
    title: 'Smart Automation Engine',
    description: 'Automate complex workflows with intelligent decision-making capabilities that learn and improve over time.'
  },
  {
    id: 4,
    icon: '🔗',
    title: 'Seamless Integrations',
    description: 'Connect with your favorite tools and platforms with our robust API designed for enterprise-grade reliability.'
  },
  {
    id: 5,
    icon: '🛡️',
    title: 'Enterprise Security',
    description: 'Bank-level security with end-to-end encryption, compliance certifications, and advanced threat protection.'
  },
  {
    id: 6,
    icon: '📊',
    title: 'Advanced Reporting',
    description: 'Comprehensive dashboards and customizable reports that provide actionable insights for data-driven decisions.'
  }
])
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

/* Features Section */
.features {
  padding: 8rem 0;
  background: linear-gradient(180deg, rgba(26, 26, 46, 0.3) 0%, rgba(22, 33, 62, 0.1) 100%);
  position: relative;
  overflow: hidden;
}

.features::before {
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

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2.5rem;
  width: 100%;
  position: relative;
  z-index: 1;
}

.feature-card {
  background: rgba(31, 31, 31, 0.4);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 24px;
  padding: 2.5rem;
  text-align: left;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
  width: 100%;
  box-sizing: border-box;
  min-height: 320px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  position: relative;
  overflow: hidden;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s ease-out forwards;
}

.feature-card::before {
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

.feature-card:hover::before {
  opacity: 1;
}

.feature-card:hover {
  transform: translateY(-15px) scale(1.02);
  border-color: rgba(0, 255, 255, 0.3);
  box-shadow: 
    0 25px 80px rgba(0, 255, 255, 0.15),
    0 0 0 1px rgba(0, 255, 255, 0.1);
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.feature-icon-wrapper {
  position: relative;
  margin-bottom: 1.5rem;
  display: inline-block;
}

.feature-icon {
  font-size: 3.5rem;
  position: relative;
  z-index: 2;
  filter: drop-shadow(0 0 20px rgba(0, 255, 255, 0.3));
}

.icon-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80px;
  height: 80px;
  background: radial-gradient(circle, rgba(0, 255, 255, 0.2) 0%, transparent 70%);
  border-radius: 50%;
  animation: pulse 3s infinite ease-in-out;
}

@keyframes pulse {
  0%, 100% { opacity: 0.5; transform: translate(-50%, -50%) scale(1); }
  50% { opacity: 1; transform: translate(-50%, -50%) scale(1.2); }
}

.feature-card h3 {
  font-size: 1.6rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #ffffff;
  position: relative;
  z-index: 2;
}

.feature-card p {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.7;
  margin-bottom: 1.5rem;
  position: relative;
  z-index: 2;
}

.feature-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #00FFFF;
  font-weight: 600;
  font-size: 0.95rem;
  transition: all 0.3s ease;
  position: relative;
  z-index: 2;
}

.feature-link:hover {
  gap: 1rem;
  color: #9A00FF;
}

.arrow-icon {
  transition: transform 0.3s ease;
}

.feature-link:hover .arrow-icon {
  transform: translateX(5px);
}

/* Responsive Design */
@media (max-width: 1024px) {
  .container {
    padding: 0 1.5rem;
  }
  
  .features-grid {
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }
  
  .feature-card {
    padding: 2rem;
    min-height: 300px;
  }
}

@media (max-width: 768px) {
  .features {
    padding: 6rem 0;
  }
  
  .features-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .feature-card {
    padding: 2rem;
    min-height: 280px;
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
  
  .feature-icon {
    font-size: 3rem;
  }
  
  .feature-card h3 {
    font-size: 1.4rem;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 1rem;
  }
  
  .feature-card {
    padding: 1.5rem;
    min-height: 260px;
  }
  
  .feature-icon {
    font-size: 2.5rem;
  }
  
  .feature-card h3 {
    font-size: 1.3rem;
  }
  
  .section-title {
    font-size: clamp(1.8rem, 7vw, 2.5rem);
    padding: 0 0.5rem;
  }
  
  .section-subtitle {
    font-size: 1rem;
    padding: 0 0.5rem;
  }
}
</style> 