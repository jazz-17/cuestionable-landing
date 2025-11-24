<template>
  <a
    :href="href"
    :class="buttonClasses"
    :target="external ? '_blank' : '_self'"
    :rel="external ? 'noopener noreferrer' : ''"
  >
    <slot></slot>
    <svg v-if="variant === 'primary'" class="transition-transform duration-200 transition-smooth group-hover:translate-x-0.5" width="16" height="16" viewBox="0 0 16 16" fill="none">
      <path d="M6 3L11 8L6 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  </a>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
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

const buttonClasses = computed(() => {
  const base = 'inline-flex items-center gap-2 rounded-lg font-semibold no-underline transition-all duration-200 transition-smooth cursor-pointer whitespace-nowrap relative overflow-hidden group';

  const variants = {
    primary: 'px-5 md:px-6 py-3 md:py-3.5 text-[15px] md:text-base bg-[var(--primary)] text-white shadow-[0_2px_4px_rgba(74,144,226,0.15)] hover:bg-[var(--primary-dark)] hover:shadow-[0_4px_8px_rgba(74,144,226,0.2)] hover:-translate-y-[1px] active:translate-y-0 active:shadow-[0_1px_3px_rgba(99,91,255,0.12)]',
    secondary: 'px-5 md:px-6 py-3 md:py-3.5 text-[15px] md:text-base bg-white text-[var(--primary)] border-[1.5px] border-[var(--border)] shadow-[var(--shadow-sm)] hover:border-[var(--primary)] hover:shadow-[var(--shadow-md)] hover:-translate-y-[1px]',
    text: 'px-0 py-2 text-[15px] md:text-base bg-transparent text-[var(--primary)] hover:text-[var(--primary-dark)]'
  };

  return `${base} ${variants[props.variant]}`;
});
</script>
