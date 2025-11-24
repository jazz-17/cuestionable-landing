<template>
  <div class="max-w-[700px] mx-auto mb-8 flex flex-col gap-3">
    <Accordion type="single" collapsible class="w-full flex flex-col gap-3">
      <AccordionItem
        v-for="(faq, index) in faqs"
        :key="index"
        :value="`item-${index}`"
        class="bg-white border border-[var(--border)] rounded-xl overflow-hidden transition-all duration-200 hover:border-[var(--primary)] reveal-on-scroll"
        :style="{ transitionDelay: `${index * 0.1}s` }"
      >
        <AccordionTrigger
          class="px-5 md:px-6 py-4 md:py-5 hover:bg-[var(--bg-secondary)] hover:no-underline data-[state=open]:bg-[rgba(158,191,166,0.05)]"
        >
          <span
            class="text-base md:text-[17px] font-semibold text-[var(--text-primary)] text-left leading-relaxed tracking-[-0.01em]"
            >{{ faq.question }}</span
          >
        </AccordionTrigger>
        <AccordionContent
          class="px-5 md:px-6 py-5 md:py-6 text-[15px] md:text-base leading-[1.7] text-[var(--text-secondary)] border-t border-[var(--border)]"
        >
          {{ faq.answer }}
        </AccordionContent>
      </AccordionItem>
    </Accordion>
  </div>
</template>

<script setup>
import {
  Accordion,
  AccordionContent,
  AccordionItem,
  AccordionTrigger,
} from "@/components/ui/accordion";

defineProps({
  faqs: {
    type: Array,
    required: true,
    default: () => [],
  },
});
</script>
