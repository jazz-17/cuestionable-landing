<template>
  <DialogRoot :open="isOpen" @update:open="handleOpenChange">
    <DialogPortal>
      <DialogOverlay class="modal-overlay" />
      <DialogContent class="modal-content">
        <DialogClose class="close-btn" aria-label="Close">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
            <path d="M5 5L15 15M15 5L5 15" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
          </svg>
        </DialogClose>

        <div class="modal-header">
          <div v-if="mentorImage" class="modal-photo">
            <img :src="imageUrl" :alt="mentorName" />
          </div>
          <div v-else class="modal-photo-placeholder">
            {{ initials }}
          </div>

          <div class="modal-title-area">
            <DialogTitle class="modal-title">{{ mentorName }}</DialogTitle>
            <div class="modal-topic">{{ mentorTopic }}</div>
            <div class="modal-rating">
              <span class="stars">{{ starsDisplay }}</span>
              <span class="rating-text">{{ mentorRating }}.0</span>
            </div>
          </div>
        </div>

        <div class="modal-body">
          <DialogDescription class="bio-text">{{ mentorBio }}</DialogDescription>
        </div>
      </DialogContent>
    </DialogPortal>
  </DialogRoot>
</template>

<script setup>
import { computed } from 'vue';
import {
  DialogRoot,
  DialogPortal,
  DialogOverlay,
  DialogContent,
  DialogTitle,
  DialogDescription,
  DialogClose
} from 'radix-vue';

const props = defineProps({
  isOpen: Boolean,
  mentorName: String,
  mentorTopic: String,
  mentorBio: String,
  mentorImage: String,
  mentorRating: Number
});

const emit = defineEmits(['close']);

const handleOpenChange = (open) => {
  if (!open) {
    emit('close');
  }
};

const imageUrl = computed(() => {
  if (!props.mentorImage) return '';
  if (props.mentorImage.startsWith('http://') || props.mentorImage.startsWith('https://')) {
    return props.mentorImage;
  }
  return `${import.meta.env.BASE_URL}${props.mentorImage}`;
});

const initials = computed(() => {
  if (!props.mentorName) return '';
  return props.mentorName
    .split(' ')
    .map(word => word[0])
    .join('')
    .toUpperCase()
    .slice(0, 2);
});

const starsDisplay = computed(() => {
  return '★'.repeat(props.mentorRating || 0) + '☆'.repeat(5 - (props.mentorRating || 0));
});
</script>

<style>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(15, 23, 42, 0.7);
  backdrop-filter: blur(4px);
  z-index: 2000;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-overlay[data-state='open'] {
  animation: overlayShow 250ms cubic-bezier(0.16, 1, 0.3, 1);
}

.modal-overlay[data-state='closed'] {
  animation: overlayHide 200ms cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes overlayShow {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes overlayHide {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}

.modal-content {
  background: white;
  border-radius: 20px;
  max-width: 500px;
  width: calc(100% - 40px);
  max-height: 90vh;
  overflow-y: auto;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
  z-index: 2001;
}

.modal-content[data-state='open'] {
  animation: contentShow 250ms cubic-bezier(0.16, 1, 0.3, 1);
}

.modal-content[data-state='closed'] {
  animation: contentHide 200ms cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes contentShow {
  from {
    opacity: 0;
    transform: translate(-50%, -48%) scale(0.96);
  }
  to {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
}

@keyframes contentHide {
  from {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
  to {
    opacity: 0;
    transform: translate(-50%, -48%) scale(0.96);
  }
}

.close-btn {
  position: absolute;
  top: 16px;
  right: 16px;
  width: 36px;
  height: 36px;
  border-radius: 8px;
  border: 1px solid var(--border);
  background: white;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
  color: var(--text-secondary);
  z-index: 1;
}

.close-btn:hover {
  border-color: var(--text-primary);
  color: var(--text-primary);
  transform: scale(1.05);
}

.modal-header {
  padding: 32px 32px 24px;
  text-align: center;
  border-bottom: 1px solid var(--border);
}

.modal-photo {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin: 0 auto 20px;
  overflow: hidden;
  border: 4px solid var(--gradient-subtle);
}

.modal-photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.modal-photo-placeholder {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin: 0 auto 20px;
  background: var(--gradient-hero);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 36px;
  font-weight: 800;
  color: white;
  font-family: 'Manrope', sans-serif;
  border: 4px solid rgba(74, 144, 226, 0.1);
}

.modal-title {
  font-size: 28px;
  font-weight: 700;
  color: var(--text-primary);
  margin: 0 0 12px 0;
  font-family: 'Manrope', sans-serif;
  letter-spacing: -0.02em;
}

.modal-topic {
  display: inline-flex;
  align-items: center;
  padding: 6px 16px;
  background: var(--gradient-subtle);
  color: var(--primary);
  font-size: 14px;
  font-weight: 600;
  border-radius: 8px;
  border: 1px solid rgba(74, 144, 226, 0.1);
  margin-bottom: 12px;
}

.modal-rating {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  color: var(--text-secondary);
  font-size: 14px;
}

.modal-rating .stars {
  color: #fbbf24;
  font-size: 16px;
  letter-spacing: 2px;
}

.modal-body {
  padding: 32px;
}

.bio-text {
  font-size: 16px;
  line-height: 1.7;
  color: var(--text-secondary);
  margin: 0;
}

@media (max-width: 768px) {
  .modal-content {
    width: 100%;
    max-width: 100%;
    max-height: 100vh;
    border-radius: 0;
    height: 100%;
    top: 50%;
    transform: translate(-50%, -50%);
  }

  .modal-content[data-state='open'] {
    animation: contentShowMobile 250ms cubic-bezier(0.16, 1, 0.3, 1);
  }

  .modal-content[data-state='closed'] {
    animation: contentHideMobile 200ms cubic-bezier(0.16, 1, 0.3, 1);
  }

  @keyframes contentShowMobile {
    from {
      opacity: 0;
      transform: translate(-50%, -50%) scale(0.98);
    }
    to {
      opacity: 1;
      transform: translate(-50%, -50%) scale(1);
    }
  }

  @keyframes contentHideMobile {
    from {
      opacity: 1;
      transform: translate(-50%, -50%) scale(1);
    }
    to {
      opacity: 0;
      transform: translate(-50%, -50%) scale(0.98);
    }
  }

  .modal-header {
    padding: 24px 24px 20px;
  }

  .modal-body {
    padding: 24px;
  }

  .modal-title {
    font-size: 24px;
  }
}
</style>
