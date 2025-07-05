<template>
  <div v-if="isOpen" class="modal-overlay" @click="closeModal">
    <div class="modal-content" @click.stop>
      <div class="modal-header">
        <h2>Get Early Access</h2>
        <button class="close-button" @click="closeModal">×</button>
      </div>
      
      <div class="modal-body">
        <div v-if="!isSubmitted" class="form-container">
          <p class="modal-description">
            Be among the first to experience the future of AI. Join our exclusive early access program and get:
          </p>
          
          <div class="benefits-list">
            <div class="benefit-item">
              <i class="benefit-icon">🚀</i>
              <span>Priority access to new features</span>
            </div>
            <div class="benefit-item">
              <i class="benefit-icon">💎</i>
              <span>Exclusive beta testing opportunities</span>
            </div>
            <div class="benefit-item">
              <i class="benefit-icon">🎁</i>
              <span>Special launch discounts</span>
            </div>
            <div class="benefit-item">
              <i class="benefit-icon">📧</i>
              <span>Early updates and announcements</span>
            </div>
          </div>
          
          <form @submit.prevent="submitForm" class="signup-form">
            <div class="form-group">
              <label for="name">Full Name</label>
              <input 
                type="text" 
                id="name" 
                v-model="formData.name" 
                :class="{ 'error': errors.name }"
                placeholder="Enter your full name"
                required
              >
              <span v-if="errors.name" class="error-message">{{ errors.name }}</span>
            </div>
            
            <div class="form-group">
              <label for="email">Email Address</label>
              <input 
                type="email" 
                id="email" 
                v-model="formData.email" 
                :class="{ 'error': errors.email }"
                placeholder="Enter your email address"
                required
              >
              <span v-if="errors.email" class="error-message">{{ errors.email }}</span>
            </div>
            
            <div class="form-group">
              <label for="company">Company (Optional)</label>
              <input 
                type="text" 
                id="company" 
                v-model="formData.company" 
                placeholder="Enter your company name"
              >
            </div>
            
            <div class="form-group checkbox-group">
              <label class="checkbox-label">
                <input 
                  type="checkbox" 
                  v-model="formData.newsletter"
                  class="checkbox-input"
                >
                <span class="checkmark"></span>
                Subscribe to our newsletter for updates and insights
              </label>
            </div>
            
            <button type="submit" class="submit-button" :disabled="isLoading">
              <span v-if="isLoading" class="loading-spinner"></span>
              {{ isLoading ? 'Joining...' : 'Join Early Access' }}
            </button>
          </form>
        </div>
        
        <div v-else class="success-container">
          <div class="success-icon">🎉</div>
          <h3>Welcome to Early Access!</h3>
          <p>Thank you for joining our exclusive early access program. We've sent a confirmation email to <strong>{{ formData.email }}</strong>.</p>
          <div class="next-steps">
            <h4>What's next?</h4>
            <ul>
              <li>Check your email for confirmation</li>
              <li>Follow us on social media for updates</li>
              <li>We'll notify you when early access begins</li>
            </ul>
          </div>
          <button @click="closeModal" class="close-success-button">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, watch } from 'vue'

// Props
const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  }
})

// Emits
const emit = defineEmits(['close'])

// Reactive data
const isSubmitted = ref(false)
const isLoading = ref(false)

const formData = reactive({
  name: '',
  email: '',
  company: '',
  newsletter: true
})

const errors = reactive({
  name: '',
  email: ''
})

// Methods
const closeModal = () => {
  emit('close')
  // Reset form after a delay to allow animation
  setTimeout(() => {
    resetForm()
  }, 300)
}

const resetForm = () => {
  formData.name = ''
  formData.email = ''
  formData.company = ''
  formData.newsletter = true
  errors.name = ''
  errors.email = ''
  isSubmitted.value = false
  isLoading.value = false
}

const validateForm = () => {
  let isValid = true
  errors.name = ''
  errors.email = ''
  
  // Name validation
  if (!formData.name.trim()) {
    errors.name = 'Name is required'
    isValid = false
  } else if (formData.name.trim().length < 2) {
    errors.name = 'Name must be at least 2 characters'
    isValid = false
  }
  
  // Email validation
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!formData.email.trim()) {
    errors.email = 'Email is required'
    isValid = false
  } else if (!emailRegex.test(formData.email)) {
    errors.email = 'Please enter a valid email address'
    isValid = false
  }
  
  return isValid
}

const submitForm = async () => {
  if (!validateForm()) return
  
  isLoading.value = true
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000))
    
    // Here you would typically send the data to your backend
    console.log('Form submitted:', formData)
    
    // Show success state
    isSubmitted.value = true
    
    // In a real app, you would send this data to your server
    // Example:
    // const response = await fetch('/api/early-access', {
    //   method: 'POST',
    //   headers: { 'Content-Type': 'application/json' },
    //   body: JSON.stringify(formData)
    // })
    
  } catch (error) {
    console.error('Error submitting form:', error)
    // Handle error state
  } finally {
    isLoading.value = false
  }
}

// Watch for modal open/close to reset form
watch(() => props.isOpen, (newValue) => {
  if (!newValue) {
    resetForm()
  }
})
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  backdrop-filter: blur(10px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
  padding: 1rem;
  animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.modal-content {
  background: rgba(31, 31, 31, 0.95);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 24px;
  max-width: 500px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  animation: slideIn 0.3s ease-out;
  position: relative;
}

@keyframes slideIn {
  from { 
    opacity: 0; 
    transform: translateY(-50px) scale(0.9);
  }
  to { 
    opacity: 1; 
    transform: translateY(0) scale(1);
  }
}

.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 2rem 2rem 1rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.modal-header h2 {
  font-size: 1.8rem;
  font-weight: 700;
  color: #ffffff;
  margin: 0;
  background: linear-gradient(135deg, #ffffff, #00FFFF);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.close-button {
  background: none;
  border: none;
  color: rgba(255, 255, 255, 0.6);
  font-size: 2rem;
  cursor: pointer;
  padding: 0;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: all 0.3s ease;
}

.close-button:hover {
  color: #ffffff;
  background: rgba(255, 255, 255, 0.1);
}

.modal-body {
  padding: 2rem;
}

.modal-description {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
  margin-bottom: 2rem;
  font-size: 1rem;
}

.benefits-list {
  margin-bottom: 2rem;
}

.benefit-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
  color: rgba(255, 255, 255, 0.9);
}

.benefit-icon {
  font-size: 1.5rem;
  min-width: 30px;
}

.signup-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  color: #ffffff;
  font-weight: 600;
  margin-bottom: 0.5rem;
  font-size: 0.95rem;
}

.form-group input {
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 12px;
  padding: 1rem;
  color: #ffffff;
  font-size: 1rem;
  transition: all 0.3s ease;
}

.form-group input::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

.form-group input:focus {
  outline: none;
  border-color: #00FFFF;
  background: rgba(0, 255, 255, 0.1);
  box-shadow: 0 0 0 3px rgba(0, 255, 255, 0.1);
}

.form-group input.error {
  border-color: #ff6b6b;
  background: rgba(255, 107, 107, 0.1);
}

.error-message {
  color: #ff6b6b;
  font-size: 0.85rem;
  margin-top: 0.5rem;
}

.checkbox-group {
  flex-direction: row;
  align-items: flex-start;
  gap: 0.75rem;
}

.checkbox-label {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  cursor: pointer;
  color: rgba(255, 255, 255, 0.8);
  font-size: 0.9rem;
  line-height: 1.4;
}

.checkbox-input {
  display: none;
}

.checkmark {
  width: 20px;
  height: 20px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 4px;
  position: relative;
  flex-shrink: 0;
  margin-top: 2px;
  transition: all 0.3s ease;
}

.checkbox-input:checked + .checkmark {
  background: #00FFFF;
  border-color: #00FFFF;
}

.checkbox-input:checked + .checkmark::after {
  content: '✓';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: #ffffff;
  font-size: 12px;
  font-weight: bold;
}

.submit-button {
  background: linear-gradient(135deg, #00FFFF, #9A00FF);
  color: #ffffff;
  border: none;
  padding: 1.2rem;
  border-radius: 12px;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 255, 255, 0.3);
}

.submit-button:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 15px 40px rgba(0, 255, 255, 0.4);
}

.submit-button:disabled {
  opacity: 0.7;
  cursor: not-allowed;
  transform: none;
}

.loading-spinner {
  display: inline-block;
  width: 16px;
  height: 16px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top-color: #ffffff;
  animation: spin 1s ease-in-out infinite;
  margin-right: 0.5rem;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

/* Success State */
.success-container {
  text-align: center;
  padding: 1rem 0;
}

.success-icon {
  font-size: 4rem;
  margin-bottom: 1rem;
  animation: bounce 0.6s ease-out;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
  40% { transform: translateY(-20px); }
  60% { transform: translateY(-10px); }
}

.success-container h3 {
  color: #ffffff;
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.success-container p {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
  margin-bottom: 2rem;
}

.next-steps {
  text-align: left;
  background: rgba(0, 255, 255, 0.1);
  border: 1px solid rgba(0, 255, 255, 0.2);
  border-radius: 12px;
  padding: 1.5rem;
  margin-bottom: 2rem;
}

.next-steps h4 {
  color: #00FFFF;
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 1rem;
}

.next-steps ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.next-steps li {
  color: rgba(255, 255, 255, 0.8);
  padding: 0.5rem 0;
  position: relative;
  padding-left: 1.5rem;
}

.next-steps li::before {
  content: '→';
  position: absolute;
  left: 0;
  color: #00FFFF;
  font-weight: bold;
}

.close-success-button {
  background: rgba(255, 255, 255, 0.1);
  color: #ffffff;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 1rem 2rem;
  border-radius: 12px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.close-success-button:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(255, 255, 255, 0.3);
}

/* Responsive Design */
@media (max-width: 768px) {
  .modal-content {
    margin: 1rem;
    max-height: 95vh;
  }
  
  .modal-header {
    padding: 1.5rem 1.5rem 1rem;
  }
  
  .modal-body {
    padding: 1.5rem;
  }
  
  .modal-header h2 {
    font-size: 1.5rem;
  }
  
  .success-icon {
    font-size: 3rem;
  }
}

@media (max-width: 480px) {
  .modal-overlay {
    padding: 0.5rem;
  }
  
  .modal-header {
    padding: 1rem 1rem 0.5rem;
  }
  
  .modal-body {
    padding: 1rem;
  }
  
  .modal-header h2 {
    font-size: 1.3rem;
  }
  
  .benefit-item {
    font-size: 0.9rem;
  }
}
</style> 