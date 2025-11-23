<template>
  <div class="mentors-carousel">
    <swiper
      :modules="modules"
      :slides-per-view="1"
      :space-between="32"
      :centered-slides="true"
      :loop="true"
      :autoplay="{
        delay: 4000,
        disableOnInteraction: false,
      }"
      :effect="'coverflow'"
      :coverflow-effect="{
        rotate: 0,
        stretch: 0,
        depth: 100,
        modifier: 2,
        slideShadows: false,
      }"
      :pagination="{
        clickable: true,
        dynamicBullets: true,
      }"
      :breakpoints="{
        768: {
          slidesPerView: 2,
          spaceBetween: 32,
        },
        1024: {
          slidesPerView: 3,
          spaceBetween: 40,
        }
      }"
      class="swiper-container"
    >
      <swiper-slide v-for="(mentor, index) in mentors" :key="index">
        <div class="mentor-card-3d">
          <div class="mentor-card-inner">
            <div class="mentor-header">
              <div class="mentor-avatar-wrapper">
                <div class="mentor-avatar">{{ mentor.initials }}</div>
                <div :class="['status-indicator', mentor.availabilityClass]"></div>
              </div>
            </div>

            <div class="mentor-content">
              <h3 class="mentor-name">{{ mentor.name }}</h3>
              <div class="mentor-topic">{{ mentor.topic }}</div>

              <div class="mentor-stats">
                <div class="stat-item">
                  <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
                    <path d="M10 1L12.5 6.5L18.5 7.5L14.5 11.5L15.5 17.5L10 14.5L4.5 17.5L5.5 11.5L1.5 7.5L7.5 6.5L10 1Z" fill="currentColor"/>
                  </svg>
                  <span>{{ mentor.rating }}.0</span>
                </div>
                <div class="stat-item">
                  <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
                    <circle cx="10" cy="10" r="8" stroke="currentColor" stroke-width="2" fill="none"/>
                    <path d="M10 6V10L13 12" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
                  </svg>
                  <span>{{ mentor.availability }}</span>
                </div>
              </div>

              <div class="mentor-specialties">
                <span v-for="(specialty, i) in mentor.specialties" :key="i" class="specialty-tag">
                  {{ specialty }}
                </span>
              </div>

              <button class="mentor-btn" @click="handleMentorClick">
                <span>Solicitar mentoría</span>
                <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
                  <path d="M6 3L11 8L6 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </button>
            </div>
          </div>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Autoplay, Pagination, EffectCoverflow } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/effect-coverflow';
import 'swiper/css/pagination';

const modules = [Autoplay, Pagination, EffectCoverflow];

const mentors = [
  {
    name: 'Adrian Zamudio',
    topic: 'Marketing Digital',
    availability: 'Disponible',
    rating: 5,
    initials: 'AZ',
    availabilityClass: 'available',
    specialties: ['Google Ads', 'SEO', 'Analytics']
  },
  {
    name: 'Maribel Bartolo',
    topic: 'Recursos Humanos',
    availability: 'Disponible',
    rating: 5,
    initials: 'MB',
    availabilityClass: 'available',
    specialties: ['Recruiting', 'Culture', 'Leadership']
  },
  {
    name: 'Nicole Quispe',
    topic: 'Tecnología & BI',
    availability: 'Disponible',
    rating: 4,
    initials: 'NQ',
    availabilityClass: 'available',
    specialties: ['Power BI', 'SQL', 'Tableau']
  }
];

const handleMentorClick = () => {
  window.open('https://forms.gle/JdC6fM1Fazotx6b6A', '_blank');
};
</script>

<style scoped>
.mentors-carousel {
  width: 100%;
  padding: 40px 0 80px 0;
}

.swiper-container {
  overflow: visible;
  padding: 20px 0;
}

.mentor-card-3d {
  height: 100%;
  perspective: 1000px;
}

.mentor-card-inner {
  background: white;
  border: 1px solid var(--border);
  border-radius: 24px;
  padding: 32px;
  height: 100%;
  display: flex;
  flex-direction: column;
  gap: 24px;
  box-shadow: var(--shadow-lg);
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  position: relative;
  overflow: hidden;
}

.mentor-card-inner::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 6px;
  background: var(--gradient-2);
}

.swiper-slide-active .mentor-card-inner {
  transform: scale(1.05);
  box-shadow: var(--shadow-xl);
  border-color: rgba(99, 91, 255, 0.3);
}

.mentor-header {
  display: flex;
  justify-content: center;
}

.mentor-avatar-wrapper {
  position: relative;
}

.mentor-avatar {
  width: 80px;
  height: 80px;
  border-radius: 20px;
  background: var(--gradient-2);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 28px;
  font-weight: 700;
  font-family: 'Manrope', sans-serif;
  box-shadow: 0 8px 24px rgba(99, 91, 255, 0.3);
}

.status-indicator {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 3px solid white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.status-indicator.available {
  background: #10b981;
}

.mentor-content {
  display: flex;
  flex-direction: column;
  gap: 16px;
  text-align: center;
}

.mentor-name {
  font-size: 24px;
  font-weight: 700;
  color: var(--text-primary);
  margin: 0;
}

.mentor-topic {
  display: inline-block;
  padding: 6px 16px;
  background: var(--gradient-3);
  color: var(--primary);
  font-size: 14px;
  font-weight: 600;
  border-radius: 8px;
  margin: 0 auto;
}

.mentor-stats {
  display: flex;
  justify-content: center;
  gap: 24px;
  padding: 16px 0;
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
}

.stat-item {
  display: flex;
  align-items: center;
  gap: 6px;
  color: var(--text-secondary);
  font-size: 14px;
  font-weight: 500;
}

.stat-item svg {
  color: #fbbf24;
}

.mentor-specialties {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: center;
}

.specialty-tag {
  padding: 4px 12px;
  background: var(--bg-secondary);
  color: var(--text-secondary);
  font-size: 12px;
  font-weight: 600;
  border-radius: 6px;
}

.mentor-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 14px 24px;
  background: var(--primary);
  color: white;
  border: none;
  border-radius: 12px;
  font-size: 15px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
  font-family: inherit;
  box-shadow: 0 4px 12px rgba(99, 91, 255, 0.2);
}

.mentor-btn:hover {
  background: var(--primary-dark);
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(99, 91, 255, 0.3);
}

.mentor-btn svg {
  transition: transform 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.mentor-btn:hover svg {
  transform: translateX(2px);
}

:deep(.swiper-pagination) {
  bottom: 20px;
}

:deep(.swiper-pagination-bullet) {
  background: var(--primary);
  opacity: 0.3;
  width: 10px;
  height: 10px;
  transition: all 0.3s;
}

:deep(.swiper-pagination-bullet-active) {
  opacity: 1;
  transform: scale(1.3);
}

@media (max-width: 768px) {
  .mentor-card-inner {
    padding: 24px;
  }

  .mentor-avatar {
    width: 64px;
    height: 64px;
    font-size: 24px;
  }

  .mentor-name {
    font-size: 20px;
  }
}
</style>
