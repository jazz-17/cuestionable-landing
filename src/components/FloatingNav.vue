<template>
  <nav :class="['floating-nav', { 'visible': isVisible }]">
    <div class="nav-container">
      <div class="nav-brand">
        <span class="brand-icon">✦</span>
        <span class="brand-text">CuestionaBle</span>
      </div>

      <div class="nav-links">
        <a href="#como-funciona" class="nav-link">Proceso</a>
        <a href="#mentores" class="nav-link">Mentores</a>
        <a href="#faq" class="nav-link">FAQ</a>
      </div>

      <a :href="formUrl" target="_blank" class="nav-cta">
        <span>Solicitar mentoría</span>
        <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
          <path d="M6 3L11 8L6 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </a>
    </div>
  </nav>
</template>

<script setup>
import { ref } from 'vue';

defineProps({
  formUrl: {
    type: String,
    required: true
  }
});

const isVisible = ref(true);
</script>

<style scoped>
.floating-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  transform: translateY(-100%);
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

.floating-nav.visible {
  transform: translateY(0);
}

.nav-container {
  max-width: 1280px;
  margin: 16px auto;
  padding: 12px 24px;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(12px) saturate(180%);
  border: 1px solid var(--border);
  border-radius: 16px;
  box-shadow: var(--shadow-lg);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-brand {
  display: flex;
  align-items: center;
  gap: 8px;
  font-weight: 700;
  font-size: 18px;
  color: var(--text-primary);
  font-family: 'Manrope', sans-serif;
}

.brand-icon {
  font-size: 20px;
  color: var(--primary);
}

.nav-links {
  display: flex;
  gap: 32px;
}

.nav-link {
  color: var(--text-secondary);
  text-decoration: none;
  font-size: 15px;
  font-weight: 500;
  transition: color 0.2s;
  position: relative;
}

.nav-link:hover {
  color: var(--primary);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  right: 0;
  height: 2px;
  background: var(--primary);
  transform: scaleX(0);
  transition: transform 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.nav-link:hover::after {
  transform: scaleX(1);
}

.nav-cta {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 10px 20px;
  background: var(--primary);
  color: white;
  border-radius: 8px;
  text-decoration: none;
  font-weight: 600;
  font-size: 14px;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.nav-cta:hover {
  background: var(--primary-dark);
  transform: translateY(-1px);
}

.nav-cta svg {
  transition: transform 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.nav-cta:hover svg {
  transform: translateX(2px);
}

@media (max-width: 768px) {
  .nav-container {
    margin: 12px;
    padding: 10px 16px;
  }

  .nav-links {
    display: none;
  }

  .brand-text {
    font-size: 16px;
  }

  .nav-cta {
    padding: 8px 16px;
    font-size: 13px;
  }
}
</style>
