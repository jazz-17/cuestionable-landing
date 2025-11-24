<template>
  <section
    id="como-funciona"
    class="process relative py-20 md:py-24 bg-[var(--bg-secondary)]"
  >
    <div class="container">
      <div class="section-header reveal-on-scroll">
        <div class="section-badge">Proceso</div>
        <h2 class="section-title">Cómo funciona</h2>
      </div>

      <div class="max-w-[800px] mx-auto flex flex-col gap-6">
        <div
          v-for="(step, index) in steps"
          :key="index"
          class="reveal-on-scroll"
          :style="{ transitionDelay: `${index * 0.1}s` }"
        >
          <StepCard
            :number="step.number"
            :title="step.title"
            :description="step.description"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import StepCard from "@/components/StepCard.vue";

defineProps({
  steps: {
    type: Array,
    required: true,
  },
});
</script>
