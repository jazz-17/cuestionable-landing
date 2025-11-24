<template>
  <DialogRoot :open="isOpen" @update:open="handleOpenChange">
    <DialogPortal>
      <DialogOverlay class="modal-overlay fixed inset-0 bg-slate-900/70 backdrop-blur-sm z-[2000] flex items-center justify-center" />
      <DialogContent class="modal-content bg-white rounded-[20px] max-w-[500px] w-[calc(100%-40px)] max-h-[90vh] overflow-y-auto fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 shadow-[0_20px_25px_-5px_rgba(0,0,0,0.1),0_10px_10px_-5px_rgba(0,0,0,0.04)] z-[2001] md:w-full md:max-w-full md:max-h-full md:rounded-none md:h-full">
        <DialogClose class="absolute top-4 right-4 w-9 h-9 rounded-lg border border-[var(--border)] bg-white flex items-center justify-center cursor-pointer transition-all duration-200 transition-smooth text-[var(--text-secondary)] z-[1] hover:border-[var(--text-primary)] hover:text-[var(--text-primary)] hover:scale-105" aria-label="Close">
          <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
            <path d="M5 5L15 15M15 5L5 15" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
          </svg>
        </DialogClose>

        <div class="p-6 md:p-8 pb-5 md:pb-6 text-center border-b border-[var(--border)]">
          <div v-if="mentorImage" class="w-[100px] h-[100px] rounded-full mx-auto mb-5 overflow-hidden border-4 border-[rgba(74,144,226,0.1)]">
            <img :src="imageUrl" :alt="mentorName" class="w-full h-full object-cover" />
          </div>
          <div v-else class="w-[100px] h-[100px] rounded-full mx-auto mb-5 bg-gradient-hero flex items-center justify-center text-4xl font-extrabold text-white font-[Manrope,sans-serif] border-4 border-[rgba(74,144,226,0.1)]">
            {{ initials }}
          </div>

          <div>
            <DialogTitle class="text-2xl md:text-[28px] font-bold text-[var(--text-primary)] m-0 mb-3 font-[Manrope,sans-serif] tracking-[-0.02em]">{{ mentorName }}</DialogTitle>
            <div class="inline-flex items-center px-4 py-1.5 bg-gradient-subtle text-[var(--primary)] text-sm font-semibold rounded-lg border border-[rgba(74,144,226,0.1)] mb-3">{{ mentorTopic }}</div>
            <div class="flex items-center justify-center gap-2 text-[var(--text-secondary)] text-sm">
              <span class="text-amber-400 text-base tracking-[2px]">{{ starsDisplay }}</span>
              <span>{{ mentorRating }}.0</span>
            </div>
          </div>
        </div>

        <div class="p-6 md:p-8">
          <DialogDescription class="text-base leading-[1.7] text-[var(--text-secondary)] m-0">{{ mentorBio }}</DialogDescription>
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
.modal-overlay[data-state='open'] {
  animation: overlayShow 250ms cubic-bezier(0.16, 1, 0.3, 1);
}
.modal-overlay[data-state='closed'] {
  animation: overlayHide 200ms cubic-bezier(0.16, 1, 0.3, 1);
}
.modal-content[data-state='open'] {
  animation: contentShow 250ms cubic-bezier(0.16, 1, 0.3, 1);
}
.modal-content[data-state='closed'] {
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
  from { opacity: 0; transform: translate(-50%, -48%) scale(0.96); }
  to { opacity: 1; transform: translate(-50%, -50%) scale(1); }
}
@keyframes contentHide {
  from { opacity: 1; transform: translate(-50%, -50%) scale(1); }
  to { opacity: 0; transform: translate(-50%, -48%) scale(0.96); }
}

@media (max-width: 768px) {
  .modal-content[data-state='open'] {
    animation: contentShowMobile 250ms cubic-bezier(0.16, 1, 0.3, 1);
  }
  .modal-content[data-state='closed'] {
    animation: contentHideMobile 200ms cubic-bezier(0.16, 1, 0.3, 1);
  }
  @keyframes contentShowMobile {
    from { opacity: 0; transform: translate(-50%, -50%) scale(0.98); }
    to { opacity: 1; transform: translate(-50%, -50%) scale(1); }
  }
  @keyframes contentHideMobile {
    from { opacity: 1; transform: translate(-50%, -50%) scale(1); }
    to { opacity: 0; transform: translate(-50%, -50%) scale(0.98); }
  }
}
</style>
