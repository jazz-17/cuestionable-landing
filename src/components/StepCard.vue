<template>
  <Card
    class="flex flex-row gap-4 md:gap-5 p-6 md:p-8 transition-all duration-300 hover:border-[rgba(74,144,226,0.3)] hover:shadow-[var(--shadow-md)] hover:-translate-y-0.5"
  >
    <div
      class="shrink-0 w-10 md:w-12 h-10 md:h-12 flex items-center justify-center rounded-[10px] bg-gradient-subtle text-[var(--primary)] text-xl md:text-2xl font-bold font-[Manrope,sans-serif]"
    >
      {{ number }}
    </div>
    <div class="flex-1">
      <h3
        class="text-lg md:text-xl font-bold text-[var(--text-primary)] mb-2 tracking-[-0.01em]"
      >
        {{ title }}
      </h3>
      <p
        class="text-[15px] md:text-base leading-relaxed text-[var(--text-secondary)] m-0"
      >
        {{ description }}
      </p>
    </div>
  </Card>
</template>

<script setup>
import { Card } from "@/components/ui/card";

defineProps({
  number: {
    type: Number,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    required: true,
  },
});
</script>
