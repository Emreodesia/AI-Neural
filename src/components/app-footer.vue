<template>
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
</template>

<script setup>
// Footer component - no additional logic needed
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

.brand-text {
  font-size: 1.5rem;
  font-weight: 700;
  color: #ffffff;
}

.accent {
  color: #00FFFF;
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

/* Responsive Design */
@media (max-width: 1024px) {
  .container {
    padding: 0 1.5rem;
  }
}

@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 2rem;
  }
  
  .footer-links {
    justify-content: center;
    flex-direction: column;
    gap: 2rem;
  }
  
  .link-group {
    text-align: center;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 1rem;
  }
}
</style> 