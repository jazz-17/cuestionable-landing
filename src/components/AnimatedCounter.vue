<template>
  <div ref="counterRef" class="counter">
    <div class="counter-number">{{ displayValue }}{{ suffix }}</div>
    <div class="counter-label">{{ label }}</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useIntersectionObserver } from '@vueuse/core';

const props = defineProps({
  end: {
    type: Number,
    required: true
  },
  duration: {
    type: Number,
    default: 2000
  },
  label: {
    type: String,
    required: true
  },
  suffix: {
    type: String,
    default: ''
  },
  decimals: {
    type: Number,
    default: 0
  }
});

const counterRef = ref(null);
const displayValue = ref(0);
const hasAnimated = ref(false);

const animateCounter = () => {
  if (hasAnimated.value) return;
  hasAnimated.value = true;

  const startTime = performance.now();
  const startValue = 0;

  const animate = (currentTime) => {
    const elapsed = currentTime - startTime;
    const progress = Math.min(elapsed / props.duration, 1);

    // Easing function
    const easeOutQuart = 1 - Math.pow(1 - progress, 4);
    const current = startValue + (props.end - startValue) * easeOutQuart;

    displayValue.value = props.decimals > 0
      ? current.toFixed(props.decimals)
      : Math.floor(current);

    if (progress < 1) {
      requestAnimationFrame(animate);
    } else {
      displayValue.value = props.decimals > 0
        ? props.end.toFixed(props.decimals)
        : props.end;
    }
  };

  requestAnimationFrame(animate);
};

onMounted(() => {
  useIntersectionObserver(
    counterRef,
    ([{ isIntersecting }]) => {
      if (isIntersecting) {
        animateCounter();
      }
    },
    { threshold: 0.5 }
  );
});
</script>

<style scoped>
.counter {
  text-align: center;
}

.counter-number {
  font-size: 48px;
  font-weight: 700;
  color: var(--primary);
  font-family: 'Manrope', sans-serif;
  line-height: 1;
  margin-bottom: 12px;
}

.counter-label {
  font-size: 16px;
  color: var(--text-tertiary);
  font-weight: 500;
}

@media (max-width: 768px) {
  .counter-number {
    font-size: 36px;
  }

  .counter-label {
    font-size: 14px;
  }
}
</style>
