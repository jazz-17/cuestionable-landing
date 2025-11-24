<template>
  <div class="w-full pb-[60px]">
    <swiper
      :modules="modules"
      :slides-per-view="1"
      :space-between="24"
      :loop="true"
      :autoplay="{
        delay: 5000,
        disableOnInteraction: false,
      }"
      :pagination="{
        clickable: true,
        dynamicBullets: true,
      }"
      :breakpoints="{
        768: {
          slidesPerView: 2,
          spaceBetween: 24,
        },
        1024: {
          slidesPerView: 3,
          spaceBetween: 32,
        }
      }"
      class="!overflow-visible"
    >
      <swiper-slide v-for="(testimonial, index) in testimonials" :key="index">
        <div class="bg-white/60 backdrop-blur-xl backdrop-saturate-[180%] border border-white/80 rounded-[20px] p-6 md:p-8 h-full flex flex-col gap-5 shadow-[0_8px_32px_rgba(10,37,64,0.06)] transition-all duration-300 transition-smooth relative overflow-hidden hover:-translate-y-1 hover:shadow-[0_8px_24px_rgba(15,23,42,0.08)] hover:border-[rgba(74,144,226,0.3)] before:content-[''] before:absolute before:inset-0 before:bg-gradient-hero before:opacity-[0.02] before:pointer-events-none">
          <div class="opacity-60">
            <svg width="32" height="32" viewBox="0 0 32 32" fill="none">
              <path d="M10 18C10 15.7909 11.7909 14 14 14V11C10.134 11 7 14.134 7 18C7 21.866 10.134 25 14 25H17V18H10Z" fill="url(#quote-gradient)"/>
              <path d="M21 18C21 15.7909 22.7909 14 25 14V11C21.134 11 18 14.134 18 18C18 21.866 21.134 25 25 25H28V18H21Z" fill="url(#quote-gradient)"/>
              <defs>
                <linearGradient id="quote-gradient" x1="7" y1="11" x2="28" y2="25" gradientUnits="userSpaceOnUse">
                  <stop stop-color="#635bff"/>
                  <stop offset="1" stop-color="#7c3aed"/>
                </linearGradient>
              </defs>
            </svg>
          </div>

          <p class="text-base leading-[1.7] text-[var(--text-primary)] flex-1 font-medium">{{ testimonial.text }}</p>

          <div class="flex items-center gap-3">
            <div class="w-12 h-12 rounded-xl bg-gradient-hero text-white flex items-center justify-center font-bold text-base font-[Manrope,sans-serif]">{{ testimonial.initials }}</div>
            <div class="flex-1">
              <div class="font-semibold text-[var(--text-primary)] text-[15px]">{{ testimonial.name }}</div>
              <div class="text-sm text-[var(--text-tertiary)]">{{ testimonial.role }}</div>
            </div>
          </div>

          <div class="flex gap-1">
            <span v-for="i in 5" :key="i" class="text-amber-400 text-base">★</span>
          </div>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Autoplay, Pagination } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/pagination';

const modules = [Autoplay, Pagination];

const testimonials = [
  {
    text: 'La mentoría transformó completamente mi carrera. Ahora domino Power BI y conseguí un aumento del 40%.',
    name: 'Carlos Mendoza',
    role: 'Analista de Datos',
    initials: 'CM'
  },
  {
    text: 'Excelente experiencia. Mi mentor me ayudó a optimizar mi CV y preparar entrevistas. Recibí 3 ofertas en un mes.',
    name: 'Sofia Torres',
    role: 'Marketing Manager',
    initials: 'ST'
  },
  {
    text: 'La mejor inversión que he hecho. Aprendí estrategias de RRHH que aplico diariamente en mi trabajo.',
    name: 'Diego Ramirez',
    role: 'HR Specialist',
    initials: 'DR'
  },
  {
    text: 'Mi mentor me guió paso a paso en mi proyecto de BI. Los resultados superaron todas mis expectativas.',
    name: 'Ana Garcia',
    role: 'Business Analyst',
    initials: 'AG'
  }
];
</script>

<style scoped>
:deep(.swiper-pagination) {
  bottom: 0;
}

:deep(.swiper-pagination-bullet) {
  background: var(--primary);
  opacity: 0.3;
  transition: all 0.3s;
}

:deep(.swiper-pagination-bullet-active) {
  opacity: 1;
  transform: scale(1.2);
}
</style>
