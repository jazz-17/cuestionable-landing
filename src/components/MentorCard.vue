<template>
  <div class="mentor-card">
    <div class="mentor-photo-wrapper">
      <img
        v-if="image"
        :src="imageUrl"
        :alt="name"
        class="mentor-photo"
      />
      <div v-else class="mentor-photo-placeholder">{{ initials }}</div>
      <div :class="['status-indicator', availabilityClass]"></div>
    </div>

    <div class="mentor-content">
      <div class="mentor-header">
        <div class="header-top">
          <h3 class="mentor-name">{{ name }}</h3>
          <button
            v-if="bio"
            class="info-btn"
            @click="showBioModal"
            aria-label="View mentor bio"
          >
            <svg
              width="16"
              height="16"
              viewBox="0 0 16 16"
              fill="none"
            >
              <circle cx="8" cy="8" r="7" stroke="currentColor" stroke-width="1.5"/>
              <path d="M8 7V11" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
              <circle cx="8" cy="5" r="0.5" fill="currentColor"/>
            </svg>
          </button>
        </div>
        <div class="mentor-topic">{{ topic }}</div>
      </div>

      <div class="mentor-stats">
        <div class="stat">
          <div class="stat-label">Disponibilidad</div>
          <div :class="['stat-value', availabilityClass]">{{ availability }}</div>
        </div>
        <div class="stat">
          <div class="stat-label">Valoración</div>
          <div class="stat-value">
            <div class="rating">
              <span class="rating-number">{{ rating }}.0</span>
              <div class="stars">{{ starsDisplay }}</div>
            </div>
          </div>
        </div>
      </div>

      <button class="mentor-btn" @click="handleClick">
        <span>{{ buttonText }}</span>
        <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
          <path d="M6 3L11 8L6 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

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
  // If image starts with http:// or https://, use it directly (external URL)
  if (props.image.startsWith('http://') || props.image.startsWith('https://')) {
    return props.image;
  }
  // Otherwise, prepend the base URL for local images in public folder
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

<style scoped>
.mentor-card {
  background: white;
  border: 1px solid var(--border);
  border-radius: 16px;
  overflow: hidden;
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  display: flex;
  flex-direction: column;
  height: 100%;
}

.mentor-card:hover {
  border-color: rgba(74, 144, 226, 0.3);
  box-shadow: var(--shadow-lg);
  transform: translateY(-4px);
}

.mentor-photo-wrapper {
  position: relative;
  width: 100%;
  aspect-ratio: 1;
  overflow: hidden;
  background: var(--gradient-hero);
}

.mentor-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.mentor-photo-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 64px;
  font-weight: 800;
  color: white;
  font-family: 'Manrope', sans-serif;
}

.status-indicator {
  position: absolute;
  bottom: 12px;
  right: 12px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: 3px solid white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.status-indicator.available {
  background: #10b981;
}

.status-indicator.unavailable {
  background: #8898aa;
}

.mentor-content {
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 20px;
  flex: 1;
}

.mentor-header {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.header-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
}

.mentor-name {
  font-size: 22px;
  font-weight: 700;
  color: var(--text-primary);
  margin: 0;
  letter-spacing: -0.02em;
  font-family: 'Manrope', sans-serif;
  flex: 1;
}

.info-btn {
  width: 32px;
  height: 32px;
  border-radius: 8px;
  border: 1px solid var(--border);
  background: white;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
  flex-shrink: 0;
  color: var(--text-secondary);
}

.info-btn:hover {
  border-color: var(--primary);
  background: rgba(74, 144, 226, 0.03);
  color: var(--primary);
  transform: scale(1.05);
}

.mentor-topic {
  display: inline-flex;
  align-items: center;
  padding: 6px 14px;
  background: var(--gradient-subtle);
  color: var(--primary);
  font-size: 13px;
  font-weight: 600;
  border-radius: 8px;
  align-self: flex-start;
  border: 1px solid rgba(74, 144, 226, 0.1);
}

.mentor-stats {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
  padding-top: 16px;
  border-top: 1px solid var(--border);
}

.stat {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.stat-label {
  font-size: 13px;
  color: var(--text-tertiary);
  font-weight: 500;
}

.stat-value {
  font-size: 15px;
  font-weight: 600;
  color: var(--text-primary);
}

.stat-value.available {
  color: #10b981;
}

.stat-value.unavailable {
  color: var(--text-tertiary);
}

.rating {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.rating-number {
  font-size: 15px;
  font-weight: 600;
  color: var(--text-primary);
}

.stars {
  font-size: 14px;
  color: #fbbf24;
  letter-spacing: 1px;
}

.mentor-btn {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 24px;
  background: white;
  color: var(--primary);
  border: 1.5px solid var(--border);
  border-radius: 8px;
  font-size: 15px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
  font-family: inherit;
}

.mentor-btn:hover {
  border-color: var(--primary);
  box-shadow: var(--shadow-md);
  transform: translateY(-1px);
}

.mentor-btn svg {
  transition: transform 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.mentor-btn:hover svg {
  transform: translateX(2px);
}

@media (max-width: 768px) {
  .mentor-content {
    padding: 20px;
  }

  .mentor-name {
    font-size: 20px;
  }

  .mentor-stats {
    grid-template-columns: 1fr;
    gap: 12px;
  }
}
</style>
