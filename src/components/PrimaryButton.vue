<template>
  <a
    :href="href"
    :class="['btn', variant]"
    :target="external ? '_blank' : '_self'"
    :rel="external ? 'noopener noreferrer' : ''"
  >
    <slot></slot>
    <svg v-if="variant === 'primary'" class="arrow" width="16" height="16" viewBox="0 0 16 16" fill="none">
      <path d="M6 3L11 8L6 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  </a>
</template>

<script setup>
defineProps({
  href: {
    type: String,
    required: true
  },
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['primary', 'secondary', 'text'].includes(value)
  },
  external: {
    type: Boolean,
    default: false
  }
});
</script>

<style scoped>
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 14px 24px;
  border-radius: 8px;
  font-weight: 600;
  font-size: 16px;
  text-decoration: none;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
  cursor: pointer;
  white-space: nowrap;
  position: relative;
  overflow: hidden;
}

.btn.primary {
  background: var(--primary);
  color: white;
  box-shadow: 0 2px 4px rgba(74, 144, 226, 0.15);
}

.btn.primary:hover {
  background: var(--primary-dark);
  box-shadow: 0 4px 8px rgba(74, 144, 226, 0.2);
  transform: translateY(-1px);
}

.btn.primary:active {
  transform: translateY(0);
  box-shadow: 0 1px 3px rgba(99, 91, 255, 0.12);
}

.btn.secondary {
  background: white;
  color: var(--primary);
  border: 1.5px solid var(--border);
  box-shadow: var(--shadow-sm);
}

.btn.secondary:hover {
  border-color: var(--primary);
  box-shadow: var(--shadow-md);
  transform: translateY(-1px);
}

.btn.text {
  background: transparent;
  color: var(--primary);
  padding: 8px 0;
}

.btn.text:hover {
  color: var(--primary-dark);
}

.arrow {
  transition: transform 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.btn.primary:hover .arrow {
  transform: translateX(2px);
}

@media (max-width: 768px) {
  .btn {
    padding: 12px 20px;
    font-size: 15px;
  }
}
</style>
