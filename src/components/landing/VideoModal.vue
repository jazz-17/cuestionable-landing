<template>
  <DialogRoot :open="isOpen" @update:open="handleOpenChange">
    <DialogPortal>
      <DialogOverlay class="video-overlay fixed inset-0 bg-black/95 z-[9998] backdrop-blur-sm" />
      <DialogContent class="video-modal fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[90vw] md:w-[95vw] max-w-[1400px] z-[9999]">
        <DialogClose class="absolute -top-[50px] right-0 md:right-1/2 md:translate-x-1/2 md:-top-[60px] w-11 h-11 rounded-full border-2 border-white/30 bg-white/10 backdrop-blur-lg text-white cursor-pointer flex items-center justify-center transition-all duration-200 transition-smooth z-[1] hover:bg-white/20 hover:border-white/60 hover:scale-110" aria-label="Cerrar">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M18 6L6 18M6 6L18 18" stroke-linecap="round"/>
          </svg>
        </DialogClose>

        <div class="w-full aspect-video bg-black rounded-xl md:rounded-lg overflow-hidden shadow-[0_25px_50px_-12px_rgba(0,0,0,0.5)]">
          <iframe
            v-if="videoId"
            width="100%"
            height="100%"
            :src="`https://www.youtube.com/embed/${videoId}?autoplay=1`"
            title="YouTube video player"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
            class="w-full h-full border-none"
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
.video-overlay[data-state='open'] {
  animation: overlayShow 300ms cubic-bezier(0.16, 1, 0.3, 1);
}
.video-overlay[data-state='closed'] {
  animation: overlayHide 200ms cubic-bezier(0.16, 1, 0.3, 1);
}
.video-modal[data-state='open'] {
  animation: contentShow 300ms cubic-bezier(0.16, 1, 0.3, 1);
}
.video-modal[data-state='closed'] {
  animation: contentHide 200ms cubic-bezier(0.16, 1, 0.3, 1);
}

@keyframes overlayShow {
  from { opacity: 0; }
  to { opacity: 1; }
}
@keyframes overlayHide {
  from { opacity: 1; }
  to { opacity: 0; }
}
@keyframes contentShow {
  from { opacity: 0; transform: translate(-50%, -50%) scale(0.95); }
  to { opacity: 1; transform: translate(-50%, -50%) scale(1); }
}
@keyframes contentHide {
  from { opacity: 1; transform: translate(-50%, -50%) scale(1); }
  to { opacity: 0; transform: translate(-50%, -50%) scale(0.95); }
}
</style>
