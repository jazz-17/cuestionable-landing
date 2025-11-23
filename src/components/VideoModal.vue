<template>
  <DialogRoot :open="isOpen" @update:open="handleOpenChange">
    <DialogPortal>
      <DialogOverlay class="video-overlay" />
      <DialogContent class="video-modal">
        <DialogClose class="close-button" aria-label="Cerrar">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M18 6L6 18M6 6L18 18" stroke-linecap="round"/>
          </svg>
        </DialogClose>

        <div class="video-container">
          <iframe
            v-if="videoId"
            width="100%"
            height="100%"
            :src="`https://www.youtube.com/embed/${videoId}?autoplay=1`"
            title="YouTube video player"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </div>
      </DialogContent>
    </DialogPortal>
  </DialogRoot>
</template>

<script setup>
import {
  DialogRoot,
  DialogPortal,
  DialogOverlay,
  DialogContent,
  DialogClose
} from 'radix-vue';

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  },
  videoId: {
    type: String,
    default: ''
  }
});

const emit = defineEmits(['close']);

const handleOpenChange = (open) => {
  if (!open) {
    emit('close');
  }
};
</script>

<style scoped>
.video-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
  z-index: 9998;
  backdrop-filter: blur(8px);
}

.video-overlay[data-state='open'] {
  animation: overlayShow 300ms cubic-bezier(0.16, 1, 0.3, 1);
}

.video-overlay[data-state='closed'] {
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

.video-modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 90vw;
  max-width: 1400px;
  z-index: 9999;
}

.video-modal[data-state='open'] {
  animation: contentShow 300ms cubic-bezier(0.16, 1, 0.3, 1);
}

.video-modal[data-state='closed'] {
  animation: contentHide 200ms cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes contentShow {
  from {
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.95);
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
    transform: translate(-50%, -50%) scale(0.95);
  }
}

.close-button {
  position: absolute;
  top: -50px;
  right: 0;
  width: 44px;
  height: 44px;
  border-radius: 50%;
  border: 2px solid rgba(255, 255, 255, 0.3);
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  color: white;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
  z-index: 1;
}

.close-button:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(255, 255, 255, 0.6);
  transform: scale(1.1);
}

.video-container {
  width: 100%;
  aspect-ratio: 16 / 9;
  background: #000;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
}

.video-container iframe {
  width: 100%;
  height: 100%;
  border: none;
}

@media (max-width: 768px) {
  .video-modal {
    width: 95vw;
  }

  .close-button {
    top: -60px;
    right: 50%;
    transform: translateX(50%);
  }

  .video-container {
    border-radius: 8px;
  }
}
</style>
