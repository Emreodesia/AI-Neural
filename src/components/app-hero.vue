<template>
  <section id="home" class="hero">
    <div class="hero-background">
      <div class="neural-network">
        <div class="node" v-for="i in 20" :key="i" :style="getNodeStyle(i)"></div>
        <svg class="connections">
          <defs>
            <linearGradient id="gradient" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#00FFFF" stop-opacity="0.8"/>
              <stop offset="100%" stop-color="#9A00FF" stop-opacity="0.4"/>
            </linearGradient>
          </defs>
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
        <button class="cta-primary" @click="openEarlyAccessModal">Try Our AI Now</button>
        <button class="cta-secondary">Book a Demo</button>
      </div>
    </div>
  </section>
  
  <!-- Early Access Modal -->
  <AppEarlyAccessModal 
    :is-open="isEarlyAccessModalOpen" 
    @close="closeEarlyAccessModal" 
  />
</template>

<script setup>
import { ref, onMounted } from 'vue'
import AppEarlyAccessModal from './app-early-access-modal.vue'

// Reactive data
const connections = ref([])
const isEarlyAccessModalOpen = ref(false)

// Methods
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

// Lifecycle
onMounted(() => {
  generateConnections()
})
</script>

<style scoped>
/* Hero Section */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  background: linear-gradient(135deg, #0D0D0D 0%, #1a1a2e 50%, #16213e 100%);
  padding-top: 30px; /* Header için üstten boşluk */
  padding-bottom: 80px; /* Alt boşluk */
}

.hero-background {
  position: absolute;
  top: 50px;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 80%, rgba(0, 255, 255, 0.15) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(154, 0, 255, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 40% 40%, rgba(0, 255, 255, 0.05) 0%, transparent 50%);
  animation: backgroundShift 20s ease-in-out infinite;
}

@keyframes backgroundShift {
  0%, 100% { 
    transform: scale(1) rotate(0deg);
    opacity: 1;
  }
  50% { 
    transform: scale(1.1) rotate(1deg);
    opacity: 0.8;
  }
}

.neural-network {
  position: relative;
  width: 100%;
  height: 100%;
}

.node {
  position: absolute;
  width: 6px;
  height: 6px;
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  border-radius: 50%;
  box-shadow: 
    0 0 20px #00FFFF,
    0 0 40px rgba(0, 255, 255, 0.3),
    inset 0 0 10px rgba(255, 255, 255, 0.5);
  animation: pulse 3s infinite ease-in-out;
  z-index: 1;
  filter: blur(0.5px);
}

.connections {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.connections defs {
  position: absolute;
}

.connections linearGradient {
  stop-color: #00FFFF;
  stop-opacity: 0.8;
}

.connections linearGradient stop:last-child {
  stop-color: #9A00FF;
  stop-opacity: 0.4;
}

.connection-line {
  stroke: url(#gradient);
  stroke-width: 1.5;
  animation: glow 4s infinite ease-in-out;
  filter: blur(0.5px);
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
  max-width: 900px;
  padding: 0 2rem;
  margin: 0 auto;
  width: 100%;
  box-sizing: border-box;
  animation: fadeInUp 1s ease-out 0.5s both;
  margin-top: 60px; /* İçerik için ek üst boşluk */
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.hero-title {
  font-size: clamp(2.5rem, 5vw, 4.5rem);
  font-weight: 800;
  line-height: 1.1;
  margin-bottom: 2.5rem; /* Başlık altı boşluğu artırıldı */
  letter-spacing: -0.02em;
  text-shadow: 0 0 30px rgba(0, 255, 255, 0.3);
  margin-top: 1rem; /* Başlık üstü boşluk */
}

.gradient-text {
  background: linear-gradient(135deg, #00FFFF, #9A00FF, #FF6B6B);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  display: block;
  margin-top: 0.5rem;
  background-size: 200% 200%;
  animation: gradientShift 3s ease-in-out infinite;
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.hero-subtitle {
  font-size: 1.3rem;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 4rem; /* Alt başlık altı boşluğu artırıldı */
  line-height: 1.7;
  font-weight: 400;
  max-width: 700px;
  margin-left: auto;
  margin-right: auto;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  padding: 0 1rem; /* Yanlarda padding */
}

.hero-buttons {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  flex-wrap: wrap;
  animation: fadeInUp 1s ease-out 1s both;
  margin-top: 2rem; /* Butonlar için üst boşluk */
  padding: 0 1rem; /* Yanlarda padding */
}

.cta-primary {
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  color: #ffffff;
  border: none;
  padding: 1.3rem 3rem; /* Padding artırıldı */
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 255, 255, 0.3);
  min-width: 200px; /* Minimum genişlik */
}

.cta-primary::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s;
}

.cta-primary:hover::before {
  left: 100%;
}

.cta-primary:hover {
  transform: translateY(-5px) scale(1.05);
  box-shadow: 0 20px 50px rgba(0, 255, 255, 0.5);
}

.cta-secondary {
  background: rgba(31, 31, 31, 0.6);
  color: #ffffff;
  border: 2px solid rgba(255, 255, 255, 0.3);
  padding: 1.3rem 3rem; /* Padding artırıldı */
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  backdrop-filter: blur(20px);
  position: relative;
  overflow: hidden;
  min-width: 200px; /* Minimum genişlik */
}

.cta-secondary::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(0, 255, 255, 0.1), rgba(154, 0, 255, 0.1));
  opacity: 0;
  transition: opacity 0.3s ease;
}

.cta-secondary:hover::before {
  opacity: 1;
}

.cta-secondary:hover {
  border-color: #00FFFF;
  background: rgba(0, 255, 255, 0.15);
  transform: translateY(-5px) scale(1.05);
  box-shadow: 0 15px 40px rgba(0, 255, 255, 0.2);
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero {
    padding-top: 100px; /* Mobilde daha az üst boşluk */
    padding-bottom: 60px;
  }
  
  .hero-content {
    margin-top: 40px; /* Mobilde daha az üst boşluk */
  }
  
  .hero-buttons {
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    padding: 0 1rem;
  }
  
  .cta-primary,
  .cta-secondary {
    width: 100%;
    max-width: 280px;
    padding: 1.1rem 2rem; /* Mobilde padding artırıldı */
    min-width: auto; /* Mobilde minimum genişlik kaldırıldı */
  }
  
  .hero-title {
    font-size: clamp(2rem, 6vw, 3rem);
    line-height: 1.3;
    margin-bottom: 2rem; /* Mobilde daha az boşluk */
  }
  
  .hero-subtitle {
    font-size: 1.1rem;
    padding: 0 1rem;
    margin-bottom: 3rem; /* Mobilde daha az boşluk */
  }
}

@media (max-width: 480px) {
  .hero {
    padding-top: 80px; /* Küçük ekranlarda daha az üst boşluk */
    padding-bottom: 40px;
  }
  
  .hero-content {
    padding: 0 1rem;
    margin-top: 30px; /* Küçük ekranlarda daha az üst boşluk */
  }
  
  .hero-title {
    font-size: clamp(1.8rem, 7vw, 2.5rem);
    margin-bottom: 1.5rem; /* Küçük ekranlarda daha az boşluk */
  }
  
  .hero-subtitle {
    font-size: 1rem;
    padding: 0 0.5rem;
    margin-bottom: 2.5rem; /* Küçük ekranlarda daha az boşluk */
  }
  
  .cta-primary,
  .cta-secondary {
    max-width: 250px;
    padding: 1rem 1.5rem; /* Küçük ekranlarda padding artırıldı */
    font-size: 1rem;
  }
}
</style> 