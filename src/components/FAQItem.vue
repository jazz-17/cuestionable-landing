<template>
  <div class="bg-white border border-[var(--border)] rounded-xl overflow-hidden transition-all duration-200 transition-smooth hover:border-[rgba(74,144,226,0.2)]">
    <button
      class="w-full px-5 md:px-6 py-4 md:py-5 bg-transparent border-none flex justify-between items-center cursor-pointer text-left transition-all duration-200 transition-smooth hover:bg-[var(--bg-secondary)]"
      @click="toggle"
      :aria-expanded="isOpen"
    >
      <span class="text-base md:text-[17px] font-semibold text-[var(--text-primary)] flex-1 pr-4 leading-relaxed tracking-[-0.01em]">{{ question }}</span>
      <div class="shrink-0 w-8 h-8 flex items-center justify-center bg-[var(--bg-secondary)] rounded-lg transition-all duration-200 transition-smooth">
        <svg
          :class="['text-[var(--text-tertiary)] transition-all duration-300 transition-smooth', isOpen ? 'rotate-180 text-[var(--primary)]' : '']"
          width="20"
          height="20"
          viewBox="0 0 20 20"
          fill="none"
        >
          <path
            d="M5 7.5L10 12.5L15 7.5"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </div>
    </button>

    <div v-if="isOpen" class="border-t border-[var(--border)] animate-[slideDown_0.3s_cubic-bezier(0.16,1,0.3,1)]">
      <div class="px-5 md:px-6 py-5 md:py-6 text-[15px] md:text-base leading-[1.7] text-[var(--text-secondary)]">
        <slot>{{ answer }}</slot>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

defineProps({
  question: {
    type: String,
    required: true
  },
  answer: {
    type: String,
    default: ''
  }
});

const isOpen = ref(false);

const toggle = () => {
  isOpen.value = !isOpen.value;
};
</script>
