<template>
  <div
    class="bg-white border border-[var(--border)] rounded-2xl overflow-hidden transition-all duration-300 flex flex-col h-full hover:border-[var(--primary)] hover:shadow-lg hover:-translate-y-1 group"
  >
    <div
      class="relative w-full aspect-square overflow-hidden bg-[var(--bg-secondary)]"
    >
      <img
        v-if="image"
        :src="imageUrl"
        :alt="name"
        class="w-full h-full object-cover block transition-transform duration-500 group-hover:scale-105"
      />
      <div
        v-else
        class="w-full h-full flex items-center justify-center text-[64px] font-extrabold text-[var(--primary)] font-[Manrope,sans-serif] opacity-50"
      >
        {{ initials }}
      </div>
      <div
        :class="[
          'absolute bottom-3 right-3 w-4 h-4 rounded-full border-[2px] border-white shadow-sm',
          availabilityClass === 'available' ? 'bg-emerald-500' : 'bg-slate-400',
        ]"
      ></div>
    </div>

    <div class="p-6 flex flex-col gap-5 flex-1">
      <div class="flex flex-col gap-2">
        <div class="flex items-center justify-between gap-3">
          <h3
            class="text-xl font-bold text-[var(--text-primary)] m-0 tracking-tight flex-1"
          >
            {{ name }}
          </h3>
          <button
            v-if="bio"
            class="w-8 h-8 rounded-full border border-[var(--border)] bg-white flex items-center justify-center cursor-pointer transition-all duration-200 shrink-0 text-[var(--text-secondary)] hover:border-[var(--primary)] hover:bg-[var(--primary)] hover:text-white"
            @click="showBioModal"
            aria-label="View mentor bio"
          >
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
              <circle
                cx="8"
                cy="8"
                r="7"
                stroke="currentColor"
                stroke-width="1.5"
              />
              <path
                d="M8 7V11"
                stroke="currentColor"
                stroke-width="1.5"
                stroke-linecap="round"
              />
              <circle cx="8" cy="5" r="0.5" fill="currentColor" />
            </svg>
          </button>
        </div>
        <div
          class="inline-flex items-center px-3 py-1 bg-[rgba(158,191,166,0.1)] text-[var(--primary-dark)] text-xs font-semibold rounded-full self-start"
        >
          {{ topic }}
        </div>
      </div>

      <div
        class="grid grid-cols-2 gap-4 pt-4 border-t border-[var(--border)] mt-auto"
      >
        <div class="flex flex-col gap-1">
          <div
            class="text-xs text-[var(--text-tertiary)] font-medium uppercase tracking-wider"
          >
            Disponibilidad
          </div>
          <div
            :class="[
              'text-sm font-semibold',
              availabilityClass === 'available'
                ? 'text-emerald-600'
                : 'text-[var(--text-tertiary)]',
            ]"
          >
            {{ availability }}
          </div>
        </div>
        <div class="flex flex-col gap-1">
          <div
            class="text-xs text-[var(--text-tertiary)] font-medium uppercase tracking-wider"
          >
            Valoración
          </div>
          <div class="text-sm font-semibold text-[var(--text-primary)]">
            <div class="flex items-center gap-1">
              <span>{{ rating }}</span>
              <span class="text-amber-400 text-xs">★</span>
            </div>
          </div>
        </div>
      </div>

      <button
        class="w-full flex items-center justify-center gap-2 px-6 py-3 bg-[var(--primary)] text-white rounded-xl text-[15px] font-semibold cursor-pointer transition-all duration-200 hover:bg-[var(--primary-dark)] hover:shadow-md active:translate-y-[1px]"
        @click="handleClick"
      >
        <span>{{ buttonText }}</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  topic: {
    type: String,
    required: true,
  },
  availability: {
    type: String,
    required: true,
  },
  rating: {
    type: Number,
    required: true,
  },
  image: {
    type: String,
    default: "",
  },
  bio: {
    type: String,
    default: "",
  },
  buttonText: {
    type: String,
    default: "Solicitar mentoría",
  },
});

const emit = defineEmits(["book", "showBio"]);

const showBioModal = () => {
  emit("showBio", {
    name: props.name,
    topic: props.topic,
    bio: props.bio,
    image: props.image,
    rating: props.rating,
  });
};

const imageUrl = computed(() => {
  if (props.image.startsWith("http://") || props.image.startsWith("https://")) {
    return props.image;
  }
  return `${import.meta.env.BASE_URL}${props.image}`;
});

const initials = computed(() => {
  return props.name
    .split(" ")
    .map((word) => word[0])
    .join("")
    .toUpperCase()
    .slice(0, 2);
});

const availabilityClass = computed(() => {
  return props.availability.toLowerCase() === "disponible"
    ? "available"
    : "unavailable";
});

const starsDisplay = computed(() => {
  return "★".repeat(props.rating) + "☆".repeat(5 - props.rating);
});

const handleClick = () => {
  emit("book", {
    name: props.name,
    topic: props.topic,
  });
};
</script>
