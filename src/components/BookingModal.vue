<template>
  <DialogRoot :open="isOpen" @update:open="handleOpenChange">
    <DialogPortal>
      <DialogOverlay class="modal-overlay fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-[9999] flex items-center justify-center" />
      <DialogContent class="modal-container bg-white rounded-[20px] max-w-[500px] w-[calc(100%-40px)] max-h-[90vh] overflow-y-auto fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 shadow-[0_20px_60px_rgba(15,23,42,0.2)] z-[10000] md:w-full md:max-w-full md:rounded-b-none md:max-h-[95vh] md:top-auto md:bottom-0 md:translate-y-0">
        <DialogClose class="absolute top-5 right-5 w-9 h-9 rounded-lg border-none bg-[var(--bg-secondary)] text-[var(--text-secondary)] cursor-pointer flex items-center justify-center transition-all duration-200 z-[1] hover:bg-[var(--border)] hover:text-[var(--text-primary)]" aria-label="Cerrar">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M18 6L6 18M6 6L18 18" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
          </svg>
        </DialogClose>

        <div class="p-6 md:p-8 pb-5 md:pb-6 border-b border-[var(--border)]">
          <div class="flex items-center gap-3 p-3 bg-gradient-subtle rounded-xl mb-5 border border-[rgba(74,144,226,0.1)]">
            <div class="w-10 h-10 rounded-lg bg-gradient-hero text-white flex items-center justify-center font-bold text-base font-[Manrope,sans-serif] shrink-0">{{ mentorInitials }}</div>
            <div>
              <div class="font-semibold text-[var(--text-primary)] text-[15px]">{{ mentorName }}</div>
              <div class="text-[13px] text-[var(--primary)] font-medium">{{ mentorTopic }}</div>
            </div>
          </div>
          <DialogTitle class="text-2xl md:text-[28px] font-bold text-[var(--text-primary)] m-0 mb-2">Solicitar mentoría</DialogTitle>
          <DialogDescription class="text-base text-[var(--text-secondary)] m-0">Completa tus datos y te contactaremos pronto</DialogDescription>
        </div>

        <form class="p-6 md:p-8 flex flex-col gap-5" @submit.prevent="handleSubmit">
          <div class="flex flex-col gap-2">
            <label for="name" class="text-sm font-semibold text-[var(--text-primary)]">Nombre completo</label>
            <input
              id="name"
              v-model="formData.name"
              type="text"
              class="w-full px-4 py-3 border-[1.5px] border-[var(--border)] rounded-lg text-[15px] font-inherit text-[var(--text-primary)] transition-all duration-200 bg-white focus:outline-none focus:border-[var(--primary)] focus:shadow-[0_0_0_3px_rgba(74,144,226,0.1)]"
              placeholder="Tu nombre"
              required
            />
          </div>

          <div class="flex flex-col gap-2">
            <label for="email" class="text-sm font-semibold text-[var(--text-primary)]">Correo electrónico</label>
            <input
              id="email"
              v-model="formData.email"
              type="email"
              class="w-full px-4 py-3 border-[1.5px] border-[var(--border)] rounded-lg text-[15px] font-inherit text-[var(--text-primary)] transition-all duration-200 bg-white focus:outline-none focus:border-[var(--primary)] focus:shadow-[0_0_0_3px_rgba(74,144,226,0.1)]"
              placeholder="tu@email.com"
              required
            />
          </div>

          <div class="flex flex-col gap-2">
            <label for="date" class="text-sm font-semibold text-[var(--text-primary)]">Fecha preferida</label>
            <input
              id="date"
              v-model="formData.date"
              type="date"
              class="w-full px-4 py-3 border-[1.5px] border-[var(--border)] rounded-lg text-[15px] font-inherit text-[var(--text-primary)] transition-all duration-200 bg-white focus:outline-none focus:border-[var(--primary)] focus:shadow-[0_0_0_3px_rgba(74,144,226,0.1)]"
              :min="minDate"
              required
            />
          </div>

          <div class="flex flex-col gap-2">
            <label for="message" class="text-sm font-semibold text-[var(--text-primary)]">Cuéntanos sobre tus objetivos (opcional)</label>
            <textarea
              id="message"
              v-model="formData.message"
              class="w-full px-4 py-3 border-[1.5px] border-[var(--border)] rounded-lg text-[15px] font-inherit text-[var(--text-primary)] transition-all duration-200 bg-white resize-y min-h-[100px] focus:outline-none focus:border-[var(--primary)] focus:shadow-[0_0_0_3px_rgba(74,144,226,0.1)]"
              placeholder="¿Qué te gustaría lograr con esta mentoría?"
              rows="4"
            ></textarea>
          </div>

          <button type="submit" class="w-full px-6 py-3.5 bg-[var(--primary)] text-white border-none rounded-lg text-base font-semibold cursor-pointer transition-all duration-200 transition-smooth flex items-center justify-center gap-2 font-inherit shadow-[0_2px_4px_rgba(74,144,226,0.15)] hover:bg-[var(--primary-dark)] hover:shadow-[0_4px_8px_rgba(74,144,226,0.2)] hover:-translate-y-[1px] group">
            <span>Enviar solicitud</span>
            <svg class="transition-transform duration-200 transition-smooth group-hover:translate-x-0.5" width="16" height="16" viewBox="0 0 16 16" fill="none">
              <path d="M6 3L11 8L6 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </button>
        </form>
      </DialogContent>
    </DialogPortal>
  </DialogRoot>
</template>

<script setup>
import { ref, computed } from 'vue';
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
  isOpen: {
    type: Boolean,
    default: false
  },
  mentorName: {
    type: String,
    default: ''
  },
  mentorTopic: {
    type: String,
    default: ''
  }
});

const emit = defineEmits(['close', 'submit']);

const formData = ref({
  name: '',
  email: '',
  date: '',
  message: ''
});

const minDate = computed(() => {
  const tomorrow = new Date();
  tomorrow.setDate(tomorrow.getDate() + 1);
  return tomorrow.toISOString().split('T')[0];
});

const mentorInitials = computed(() => {
  return props.mentorName
    .split(' ')
    .map(word => word[0])
    .join('')
    .toUpperCase()
    .slice(0, 2);
});

const handleOpenChange = (open) => {
  if (!open) {
    emit('close');
  }
};

const handleSubmit = () => {
  console.log('Form submitted:', {
    mentor: props.mentorName,
    ...formData.value
  });

  const params = new URLSearchParams({
    mentor: props.mentorName,
    name: formData.value.name,
    email: formData.value.email,
    date: formData.value.date,
    message: formData.value.message
  });

  window.open(`https://forms.gle/JdC6fM1Fazotx6b6A?${params.toString()}`, '_blank');

  formData.value = {
    name: '',
    email: '',
    date: '',
    message: ''
  };

  emit('close');
};
</script>

<style>
.modal-overlay[data-state='open'] {
  animation: overlayShow 250ms cubic-bezier(0.16, 1, 0.3, 1);
}
.modal-overlay[data-state='closed'] {
  animation: overlayHide 200ms cubic-bezier(0.16, 1, 0.3, 1);
}
.modal-container[data-state='open'] {
  animation: contentShow 250ms cubic-bezier(0.16, 1, 0.3, 1);
}
.modal-container[data-state='closed'] {
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
  .modal-container[data-state='open'] {
    animation: contentShowMobile 250ms cubic-bezier(0.16, 1, 0.3, 1);
  }
  .modal-container[data-state='closed'] {
    animation: contentHideMobile 200ms cubic-bezier(0.16, 1, 0.3, 1);
  }
  @keyframes contentShowMobile {
    from { opacity: 0; transform: translate(-50%, 20px); }
    to { opacity: 1; transform: translate(-50%, 0); }
  }
  @keyframes contentHideMobile {
    from { opacity: 1; transform: translate(-50%, 0); }
    to { opacity: 0; transform: translate(-50%, 20px); }
  }
}
</style>
