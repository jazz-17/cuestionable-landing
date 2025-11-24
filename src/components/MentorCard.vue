<template>
  <div class="bg-white border border-[var(--border)] rounded-2xl overflow-hidden transition-all duration-300 transition-smooth flex flex-col h-full hover:border-[rgba(74,144,226,0.3)] hover:shadow-[var(--shadow-lg)] hover:-translate-y-1">
    <div class="relative w-full aspect-square overflow-hidden bg-gradient-hero">
      <img
        v-if="image"
        :src="imageUrl"
        :alt="name"
        class="w-full h-full object-cover block"
      />
      <div v-else class="w-full h-full flex items-center justify-center text-[64px] font-extrabold text-white font-[Manrope,sans-serif]">{{ initials }}</div>
      <div :class="['absolute bottom-3 right-3 w-5 h-5 rounded-full border-[3px] border-white shadow-[0_2px_8px_rgba(0,0,0,0.15)]', availabilityClass === 'available' ? 'bg-emerald-500' : 'bg-slate-400']"></div>
    </div>

    <div class="p-5 md:p-6 flex flex-col gap-5 flex-1">
      <div class="flex flex-col gap-2">
        <div class="flex items-center justify-between gap-3">
          <h3 class="text-xl md:text-[22px] font-bold text-[var(--text-primary)] m-0 tracking-[-0.02em] font-[Manrope,sans-serif] flex-1">{{ name }}</h3>
          <button
            v-if="bio"
            class="w-8 h-8 rounded-lg border border-[var(--border)] bg-white flex items-center justify-center cursor-pointer transition-all duration-200 transition-smooth shrink-0 text-[var(--text-secondary)] hover:border-[var(--primary)] hover:bg-[rgba(74,144,226,0.03)] hover:text-[var(--primary)] hover:scale-105"
            @click="showBioModal"
            aria-label="View mentor bio"
          >
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
              <circle cx="8" cy="8" r="7" stroke="currentColor" stroke-width="1.5"/>
              <path d="M8 7V11" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
              <circle cx="8" cy="5" r="0.5" fill="currentColor"/>
            </svg>
          </button>
        </div>
        <div class="inline-flex items-center px-3.5 py-1.5 bg-gradient-subtle text-[var(--primary)] text-[13px] font-semibold rounded-lg self-start border border-[rgba(74,144,226,0.1)]">{{ topic }}</div>
      </div>

      <div class="grid grid-cols-2 md:grid-cols-1 gap-4 md:gap-3 pt-4 border-t border-[var(--border)]">
        <div class="flex flex-col gap-1">
          <div class="text-[13px] text-[var(--text-tertiary)] font-medium">Disponibilidad</div>
          <div :class="['text-[15px] font-semibold', availabilityClass === 'available' ? 'text-emerald-500' : 'text-[var(--text-tertiary)]']">{{ availability }}</div>
        </div>
        <div class="flex flex-col gap-1">
          <div class="text-[13px] text-[var(--text-tertiary)] font-medium">Valoración</div>
          <div class="text-[15px] font-semibold text-[var(--text-primary)]">
            <div class="flex flex-col gap-0.5">
              <span>{{ rating }}.0</span>
              <div class="text-sm text-amber-400 tracking-[1px]">{{ starsDisplay }}</div>
            </div>
          </div>
        </div>
      </div>

      <button class="w-full flex items-center justify-center gap-2 px-6 py-3 bg-white text-[var(--primary)] border-[1.5px] border-[var(--border)] rounded-lg text-[15px] font-semibold cursor-pointer transition-all duration-200 transition-smooth font-inherit hover:border-[var(--primary)] hover:shadow-[var(--shadow-md)] hover:-translate-y-[1px] group" @click="handleClick">
        <span>{{ buttonText }}</span>
        <svg class="transition-transform duration-200 transition-smooth group-hover:translate-x-0.5" width="16" height="16" viewBox="0 0 16 16" fill="none">
          <path d="M6 3L11 8L6 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  topic: {
    type: String,
    required: true
  },
  availability: {
    type: String,
    required: true
  },
  rating: {
    type: Number,
    required: true
  },
  image: {
    type: String,
    default: ''
  },
  bio: {
    type: String,
    default: ''
  },
  buttonText: {
    type: String,
    default: 'Solicitar mentoría'
  }
});

const emit = defineEmits(['book', 'showBio']);

const showBioModal = () => {
  emit('showBio', {
    name: props.name,
    topic: props.topic,
    bio: props.bio,
    image: props.image,
    rating: props.rating
  });
};

const imageUrl = computed(() => {
  if (props.image.startsWith('http://') || props.image.startsWith('https://')) {
    return props.image;
  }
  return `${import.meta.env.BASE_URL}${props.image}`;
});

const initials = computed(() => {
  return props.name
    .split(' ')
    .map(word => word[0])
    .join('')
    .toUpperCase()
    .slice(0, 2);
});

const availabilityClass = computed(() => {
  return props.availability.toLowerCase() === 'disponible' ? 'available' : 'unavailable';
});

const starsDisplay = computed(() => {
  return '★'.repeat(props.rating) + '☆'.repeat(5 - props.rating);
});

const handleClick = () => {
  emit('book', {
    name: props.name,
    topic: props.topic
  });
};
</script>
