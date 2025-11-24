<template>
  <nav
    :class="[
      'fixed top-0 left-0 right-0 z-10 transition-transform duration-[400ms] transition-smooth',
      isVisible ? 'translate-y-0' : '-translate-y-full',
    ]"
  >
    <div
      class="max-w-7xl mx-4 md:mx-auto mt-4 md:mt-4 px-4 md:px-6 py-3 bg-white/80 backdrop-blur-xl backdrop-saturate-[180%] border border-[var(--border)] rounded-2xl shadow-[var(--shadow-lg)] flex items-center justify-between"
    >
      <div
        class="flex items-center gap-2 font-bold text-lg text-[var(--text-primary)] font-[Manrope,sans-serif]"
      >
        <img
          src="/logo.png"
          alt="CuestionaBle Logo"
          class="h-8 w-8 object-contain rounded-lg"
        />
        <span class="text-base md:text-lg">CuestionaBle</span>
      </div>

      <div class="hidden md:flex gap-8">
        <a
          href="#como-funciona"
          class="text-[var(--text-secondary)] no-underline text-[15px] font-medium transition-colors duration-200 relative hover:text-[var(--primary)] group"
        >
          Proceso
          <span
            class="absolute -bottom-1 left-0 right-0 h-0.5 bg-[var(--primary)] scale-x-0 transition-transform duration-200 transition-smooth group-hover:scale-x-100"
          ></span>
        </a>
        <a
          href="#mentores"
          class="text-[var(--text-secondary)] no-underline text-[15px] font-medium transition-colors duration-200 relative hover:text-[var(--primary)] group"
        >
          Mentores
          <span
            class="absolute -bottom-1 left-0 right-0 h-0.5 bg-[var(--primary)] scale-x-0 transition-transform duration-200 transition-smooth group-hover:scale-x-100"
          ></span>
        </a>
        <a
          href="#faq"
          class="text-[var(--text-secondary)] no-underline text-[15px] font-medium transition-colors duration-200 relative hover:text-[var(--primary)] group"
        >
          FAQ
          <span
            class="absolute -bottom-1 left-0 right-0 h-0.5 bg-[var(--primary)] scale-x-0 transition-transform duration-200 transition-smooth group-hover:scale-x-100"
          ></span>
        </a>
      </div>

      <a
        :href="formUrl"
        target="_blank"
        class="inline-flex items-center gap-1.5 px-4 md:px-5 py-2 md:py-2.5 bg-[var(--primary)] text-white rounded-lg no-underline font-semibold text-[13px] md:text-sm transition-all duration-200 transition-smooth hover:bg-[var(--primary-dark)] hover:-translate-y-[1px] group"
      >
        <span>Solicitar mentoría</span>
        <svg
          class="transition-transform duration-200 transition-smooth group-hover:translate-x-0.5"
          width="16"
          height="16"
          viewBox="0 0 16 16"
          fill="none"
        >
          <path
            d="M6 3L11 8L6 13"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </a>
    </div>
  </nav>
</template>

<script setup>
import { ref } from "vue";

defineProps({
  formUrl: {
    type: String,
    required: true,
  },
});

const isVisible = ref(true);
</script>
