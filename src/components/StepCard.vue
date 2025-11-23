<template>
  <div class="step-card">
    <div class="step-number">{{ number }}</div>
    <div class="step-content">
      <h3 class="step-title">{{ title }}</h3>
      <p class="step-description">{{ description }}</p>
    </div>
  </div>
</template>

<script setup>
defineProps({
  number: {
    type: Number,
    required: true
  },
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  }
});
</script>

<style scoped>
.step-card {
  display: flex;
  gap: 20px;
  padding: 32px;
  background: white;
  border: 1px solid var(--border);
  border-radius: 12px;
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  position: relative;
}

.step-card:hover {
  border-color: rgba(74, 144, 226, 0.3);
  box-shadow: var(--shadow-md);
  transform: translateY(-2px);
}


.step-number {
  flex-shrink: 0;
  width: 48px;
  height: 48px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 10px;
  background: var(--gradient-subtle);
  color: var(--primary);
  font-size: 24px;
  font-weight: 700;
  font-family: 'Manrope', sans-serif;
}

.step-content {
  flex: 1;
}

.step-title {
  font-size: 20px;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 8px;
  letter-spacing: -0.01em;
}

.step-description {
  font-size: 16px;
  line-height: 1.6;
  color: var(--text-secondary);
  margin: 0;
}

@media (max-width: 768px) {
  .step-card {
    padding: 24px;
    gap: 16px;
  }

  .step-number {
    width: 40px;
    height: 40px;
    font-size: 20px;
  }

  .step-title {
    font-size: 18px;
  }

  .step-description {
    font-size: 15px;
  }
}
</style>
