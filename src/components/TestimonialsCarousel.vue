<template>
  <div class="testimonials-carousel">
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
      class="swiper-container"
    >
      <swiper-slide v-for="(testimonial, index) in testimonials" :key="index">
        <div class="testimonial-card">
          <div class="quote-icon">
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

          <p class="testimonial-text">{{ testimonial.text }}</p>

          <div class="testimonial-author">
            <div class="author-avatar">{{ testimonial.initials }}</div>
            <div class="author-info">
              <div class="author-name">{{ testimonial.name }}</div>
              <div class="author-role">{{ testimonial.role }}</div>
            </div>
          </div>

          <div class="rating">
            <span v-for="i in 5" :key="i" class="star">★</span>
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
.testimonials-carousel {
  width: 100%;
  padding: 0 0 60px 0;
}

.swiper-container {
  overflow: visible;
}

.testimonial-card {
  background: rgba(255, 255, 255, 0.6);
  backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.8);
  border-radius: 20px;
  padding: 32px;
  height: 100%;
  display: flex;
  flex-direction: column;
  gap: 20px;
  box-shadow: 0 8px 32px rgba(10, 37, 64, 0.06);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  position: relative;
  overflow: hidden;
}

.testimonial-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--gradient-hero);
  opacity: 0.02;
  pointer-events: none;
}

.testimonial-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(15, 23, 42, 0.08);
  border-color: rgba(74, 144, 226, 0.3);
}

.quote-icon {
  opacity: 0.6;
}

.testimonial-text {
  font-size: 16px;
  line-height: 1.7;
  color: var(--text-primary);
  flex: 1;
  font-weight: 500;
}

.testimonial-author {
  display: flex;
  align-items: center;
  gap: 12px;
}

.author-avatar {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  background: var(--gradient-hero);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 16px;
  font-family: 'Manrope', sans-serif;
}

.author-info {
  flex: 1;
}

.author-name {
  font-weight: 600;
  color: var(--text-primary);
  font-size: 15px;
}

.author-role {
  font-size: 14px;
  color: var(--text-tertiary);
}

.rating {
  display: flex;
  gap: 4px;
}

.star {
  color: #fbbf24;
  font-size: 16px;
}

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

@media (max-width: 768px) {
  .testimonial-card {
    padding: 24px;
  }
}
</style>
