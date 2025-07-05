<template>
  <section id="testimonials" class="testimonials">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">What Our Clients Say</h2>
        <p class="section-subtitle">Join thousands of satisfied customers who trust our AI solutions</p>
      </div>
      <div class="testimonials-grid">
        <div class="testimonial-card" v-for="(testimonial, index) in testimonials" :key="testimonial.id" :style="{ animationDelay: `${index * 0.2}s` }">
          <div class="testimonial-header">
            <div class="rating">
              <span v-for="i in 5" :key="i" class="star">★</span>
            </div>
            <div class="quote-icon">"</div>
          </div>
          <div class="testimonial-content">
            <p>{{ testimonial.content }}</p>
          </div>
          <div class="testimonial-author">
            <div class="avatar-wrapper">
              <img :src="testimonial.avatar" :alt="testimonial.name" class="avatar">
              <div class="avatar-glow"></div>
            </div>
            <div class="author-info">
              <h4>{{ testimonial.name }}</h4>
              <span>{{ testimonial.position }}</span>
              <div class="company">{{ testimonial.company }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="testimonials-stats">
        <div class="stat-item">
          <div class="stat-number">10K+</div>
          <div class="stat-label">Happy Customers</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">99.9%</div>
          <div class="stat-label">Uptime</div>
        </div>
        <div class="stat-item">
          <div class="stat-number">4.9/5</div>
          <div class="stat-label">Average Rating</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

// Testimonials data
const testimonials = ref([
  {
    id: 1,
    content: 'AINeural transformed our business operations completely. The real-time insights and automation capabilities have increased our efficiency by 300%. The team is incredibly responsive and the platform is rock-solid.',
    name: 'Sarah Chen',
    position: 'Chief Technology Officer',
    company: 'TechCorp Solutions',
    avatar: 'https://images.unsplash.com/photo-1494790108755-2616b612b786?w=80&h=80&fit=crop&crop=face'
  },
  {
    id: 2,
    content: 'The API integration was seamless and our development team was up and running in just a few hours. The documentation is excellent and the support team goes above and beyond. Highly recommended!',
    name: 'Michael Rodriguez',
    position: 'Lead Developer',
    company: 'Innovate Labs',
    avatar: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=80&h=80&fit=crop&crop=face'
  },
  {
    id: 3,
    content: 'Outstanding AI capabilities that have revolutionized our data processing. The automation engine has saved us countless hours and the accuracy is phenomenal. This is exactly what we needed.',
    name: 'Emily Johnson',
    position: 'Product Manager',
    company: 'FutureAI Systems',
    avatar: 'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=80&h=80&fit=crop&crop=face'
  },
  {
    id: 4,
    content: 'We\'ve tried many AI platforms, but AINeural stands out with its enterprise-grade security and scalability. The real-time analytics have given us insights we never had before.',
    name: 'David Kim',
    position: 'Data Science Director',
    company: 'Global Analytics',
    avatar: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=80&h=80&fit=crop&crop=face'
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

/* Testimonials Section */
.testimonials {
  padding: 8rem 0;
  background: linear-gradient(180deg, rgba(22, 33, 62, 0.2) 0%, rgba(26, 26, 46, 0.3) 100%);
  position: relative;
  overflow: hidden;
}

.testimonials::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 30% 30%, rgba(154, 0, 255, 0.05) 0%, transparent 50%),
    radial-gradient(circle at 70% 70%, rgba(0, 255, 255, 0.05) 0%, transparent 50%);
  pointer-events: none;
}

.testimonials-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2.5rem;
  width: 100%;
  position: relative;
  z-index: 1;
  margin-bottom: 4rem;
}

.testimonial-card {
  background: rgba(31, 31, 31, 0.4);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 24px;
  padding: 2.5rem;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  width: 100%;
  box-sizing: border-box;
  min-height: 300px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  position: relative;
  overflow: hidden;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s ease-out forwards;
}

.testimonial-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(154, 0, 255, 0.05), rgba(0, 255, 255, 0.05));
  opacity: 0;
  transition: opacity 0.3s ease;
}

.testimonial-card:hover::before {
  opacity: 1;
}

.testimonial-card:hover {
  transform: translateY(-10px) scale(1.02);
  border-color: rgba(154, 0, 255, 0.3);
  box-shadow: 
    0 25px 80px rgba(154, 0, 255, 0.15),
    0 0 0 1px rgba(154, 0, 255, 0.1);
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.testimonial-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1.5rem;
}

.rating {
  display: flex;
  gap: 0.2rem;
}

.star {
  color: #FFD700;
  font-size: 1.2rem;
  filter: drop-shadow(0 0 5px rgba(255, 215, 0, 0.5));
}

.quote-icon {
  font-size: 3rem;
  color: rgba(154, 0, 255, 0.3);
  font-family: serif;
  line-height: 1;
}

.testimonial-content {
  margin-bottom: 2rem;
  flex-grow: 1;
}

.testimonial-content p {
  font-style: italic;
  color: rgba(255, 255, 255, 0.9);
  line-height: 1.7;
  font-size: 1.05rem;
}

.testimonial-author {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.avatar-wrapper {
  position: relative;
}

.avatar {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid rgba(154, 0, 255, 0.3);
  position: relative;
  z-index: 2;
}

.avatar-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 70px;
  height: 70px;
  background: radial-gradient(circle, rgba(154, 0, 255, 0.2) 0%, transparent 70%);
  border-radius: 50%;
  animation: pulse 3s infinite ease-in-out;
}

@keyframes pulse {
  0%, 100% { opacity: 0.5; transform: translate(-50%, -50%) scale(1); }
  50% { opacity: 1; transform: translate(-50%, -50%) scale(1.1); }
}

.author-info h4 {
  font-weight: 700;
  color: #ffffff;
  margin-bottom: 0.2rem;
  font-size: 1.1rem;
}

.author-info span {
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
  display: block;
  margin-bottom: 0.2rem;
}

.company {
  color: #9A00FF;
  font-size: 0.85rem;
  font-weight: 600;
}

.testimonials-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
  margin-top: 4rem;
  position: relative;
  z-index: 1;
}

.stat-item {
  text-align: center;
  padding: 2rem;
  background: rgba(31, 31, 31, 0.3);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  transition: all 0.3s ease;
}

.stat-item:hover {
  transform: translateY(-5px);
  border-color: rgba(0, 255, 255, 0.3);
  box-shadow: 0 15px 40px rgba(0, 255, 255, 0.1);
}

.stat-number {
  font-size: 2.5rem;
  font-weight: 800;
  color: #00FFFF;
  margin-bottom: 0.5rem;
  text-shadow: 0 0 20px rgba(0, 255, 255, 0.3);
}

.stat-label {
  color: rgba(255, 255, 255, 0.8);
  font-size: 1rem;
  font-weight: 500;
}

/* Responsive Design */
@media (max-width: 1024px) {
  .container {
    padding: 0 1.5rem;
  }
  
  .testimonials-grid {
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 2rem;
  }
  
  .testimonial-card {
    padding: 2rem;
    min-height: 280px;
  }
  
  .testimonials-stats {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 1.5rem;
  }
}

@media (max-width: 768px) {
  .testimonials {
    padding: 6rem 0;
  }
  
  .testimonials-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }
  
  .testimonial-card {
    padding: 2rem;
    min-height: 260px;
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
  
  .testimonials-stats {
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
  }
  
  .stat-item {
    padding: 1.5rem;
  }
  
  .stat-number {
    font-size: 2rem;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 1rem;
  }
  
  .testimonial-card {
    padding: 1.5rem;
    min-height: 240px;
  }
  
  .avatar {
    width: 50px;
    height: 50px;
  }
  
  .section-title {
    font-size: clamp(1.8rem, 7vw, 2.5rem);
    padding: 0 0.5rem;
  }
  
  .section-subtitle {
    font-size: 1rem;
    padding: 0 0.5rem;
  }
  
  .testimonials-stats {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
  
  .stat-item {
    padding: 1.2rem;
  }
  
  .stat-number {
    font-size: 1.8rem;
  }
}
</style> 