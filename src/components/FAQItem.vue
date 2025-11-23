<template>
  <div class="faq-item">
    <button
      class="faq-question"
      @click="toggle"
      :aria-expanded="isOpen"
    >
      <span class="question-text">{{ question }}</span>
      <div class="icon-wrapper">
        <svg
          class="icon"
          :class="{ 'is-open': isOpen }"
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

    <div v-if="isOpen" class="faq-answer">
      <div class="answer-content">
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

<style scoped>
.faq-item {
  background: white;
  border: 1px solid var(--border);
  border-radius: 12px;
  overflow: hidden;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.faq-item:hover {
  border-color: rgba(74, 144, 226, 0.2);
}

.faq-question {
  width: 100%;
  padding: 20px 24px;
  background: transparent;
  border: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
  text-align: left;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.faq-question:hover {
  background: var(--bg-secondary);
}

.question-text {
  font-size: 17px;
  font-weight: 600;
  color: var(--text-primary);
  flex: 1;
  padding-right: 16px;
  line-height: 1.5;
  letter-spacing: -0.01em;
}

.icon-wrapper {
  flex-shrink: 0;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--bg-secondary);
  border-radius: 8px;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.faq-question:hover .icon-wrapper {
  background: rgba(74, 144, 226, 0.1);
}

.icon {
  color: var(--text-tertiary);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.icon.is-open {
  transform: rotate(180deg);
  color: var(--primary);
}

.faq-answer {
  border-top: 1px solid var(--border);
  animation: slideDown 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.answer-content {
  padding: 20px 24px 24px;
  font-size: 16px;
  line-height: 1.7;
  color: var(--text-secondary);
}

@keyframes slideDown {
  from {
    opacity: 0;
    max-height: 0;
  }
  to {
    opacity: 1;
    max-height: 500px;
  }
}

@media (max-width: 768px) {
  .faq-question {
    padding: 16px 20px;
  }

  .question-text {
    font-size: 16px;
  }

  .answer-content {
    padding: 16px 20px 20px;
    font-size: 15px;
  }
}
</style>
