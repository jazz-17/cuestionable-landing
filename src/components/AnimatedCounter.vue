<template>
  <div ref="counterRef" class="text-center">
    <div
      class="text-4xl md:text-5xl font-bold text-[var(--primary)] font-[Manrope,sans-serif] leading-none mb-3"
    >
      {{ displayValue }}{{ suffix }}
    </div>
    <div class="text-sm md:text-base text-[var(--text-tertiary)] font-medium">
      {{ label }}
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const props = defineProps({
  end: {
    type: Number,
    required: true,
  },
  duration: {
    type: Number,
    default: 2000,
  },
  label: {
    type: String,
    required: true,
  },
  suffix: {
    type: String,
    default: "",
  },
  decimals: {
    type: Number,
    default: 0,
  },
});

const counterRef = ref(null);
const displayValue = ref(0);
const hasAnimated = ref(false);
let observer = null;

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

    displayValue.value =
      props.decimals > 0
        ? current.toFixed(props.decimals)
        : Math.floor(current);

    if (progress < 1) {
      requestAnimationFrame(animate);
    } else {
      displayValue.value =
        props.decimals > 0 ? props.end.toFixed(props.decimals) : props.end;
    }
  };

  requestAnimationFrame(animate);
};

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      if (entries[0].isIntersecting) {
        animateCounter();
        if (counterRef.value) {
          observer.unobserve(counterRef.value);
        }
      }
    },
    { threshold: 0.5 }
  );

  if (counterRef.value) {
    observer.observe(counterRef.value);
  }
});

onUnmounted(() => {
  if (observer) {
    observer.disconnect();
  }
});
</script>
