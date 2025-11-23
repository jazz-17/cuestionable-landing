<template>
  <DialogRoot :open="isOpen" @update:open="handleOpenChange">
    <DialogPortal>
      <DialogOverlay class="modal-overlay" />
      <DialogContent class="modal-container">
        <DialogClose class="modal-close" aria-label="Cerrar">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
            <path d="M18 6L6 18M6 6L18 18" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
          </svg>
        </DialogClose>

        <div class="modal-header">
          <div class="mentor-badge">
            <div class="badge-avatar">{{ mentorInitials }}</div>
            <div class="badge-info">
              <div class="badge-name">{{ mentorName }}</div>
              <div class="badge-topic">{{ mentorTopic }}</div>
            </div>
          </div>
          <DialogTitle class="modal-title">Solicitar mentoría</DialogTitle>
          <DialogDescription class="modal-subtitle">Completa tus datos y te contactaremos pronto</DialogDescription>
        </div>

        <form class="modal-form" @submit.prevent="handleSubmit">
          <div class="form-group">
            <label for="name" class="form-label">Nombre completo</label>
            <input
              id="name"
              v-model="formData.name"
              type="text"
              class="form-input"
              placeholder="Tu nombre"
              required
            />
          </div>

          <div class="form-group">
            <label for="email" class="form-label">Correo electrónico</label>
            <input
              id="email"
              v-model="formData.email"
              type="email"
              class="form-input"
              placeholder="tu@email.com"
              required
            />
          </div>

          <div class="form-group">
            <label for="date" class="form-label">Fecha preferida</label>
            <input
              id="date"
              v-model="formData.date"
              type="date"
              class="form-input"
              :min="minDate"
              required
            />
          </div>

          <div class="form-group">
            <label for="message" class="form-label">Cuéntanos sobre tus objetivos (opcional)</label>
            <textarea
              id="message"
              v-model="formData.message"
              class="form-textarea"
              placeholder="¿Qué te gustaría lograr con esta mentoría?"
              rows="4"
            ></textarea>
          </div>

          <button type="submit" class="form-submit">
            <span>Enviar solicitud</span>
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
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
  // Placeholder - would normally send to backend
  console.log('Form submitted:', {
    mentor: props.mentorName,
    ...formData.value
  });

  // Redirect to actual form with pre-filled data
  const params = new URLSearchParams({
    mentor: props.mentorName,
    name: formData.value.name,
    email: formData.value.email,
    date: formData.value.date,
    message: formData.value.message
  });

  window.open(`https://forms.gle/JdC6fM1Fazotx6b6A?${params.toString()}`, '_blank');

  // Reset form
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
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(15, 23, 42, 0.6);
  backdrop-filter: blur(4px);
  z-index: 9999;
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

.modal-container {
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
  box-shadow: 0 20px 60px rgba(15, 23, 42, 0.2);
  z-index: 10000;
}

.modal-container[data-state='open'] {
  animation: contentShow 250ms cubic-bezier(0.16, 1, 0.3, 1);
}

.modal-container[data-state='closed'] {
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

.modal-close {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 36px;
  height: 36px;
  border-radius: 8px;
  border: none;
  background: var(--bg-secondary);
  color: var(--text-secondary);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s;
  z-index: 1;
}

.modal-close:hover {
  background: var(--border);
  color: var(--text-primary);
}

.modal-header {
  padding: 32px 32px 24px;
  border-bottom: 1px solid var(--border);
}

.mentor-badge {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px;
  background: var(--gradient-subtle);
  border-radius: 12px;
  margin-bottom: 20px;
  border: 1px solid rgba(74, 144, 226, 0.1);
}

.badge-avatar {
  width: 40px;
  height: 40px;
  border-radius: 8px;
  background: var(--gradient-hero);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 16px;
  font-family: 'Manrope', sans-serif;
  flex-shrink: 0;
}

.badge-name {
  font-weight: 600;
  color: var(--text-primary);
  font-size: 15px;
}

.badge-topic {
  font-size: 13px;
  color: var(--primary);
  font-weight: 500;
}

.modal-title {
  font-size: 28px;
  font-weight: 700;
  color: var(--text-primary);
  margin: 0 0 8px 0;
}

.modal-subtitle {
  font-size: 16px;
  color: var(--text-secondary);
  margin: 0;
}

.modal-form {
  padding: 32px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.form-label {
  font-size: 14px;
  font-weight: 600;
  color: var(--text-primary);
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 12px 16px;
  border: 1.5px solid var(--border);
  border-radius: 8px;
  font-size: 15px;
  font-family: inherit;
  color: var(--text-primary);
  transition: all 0.2s;
  background: white;
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 3px rgba(74, 144, 226, 0.1);
}

.form-textarea {
  resize: vertical;
  min-height: 100px;
}

.form-submit {
  width: 100%;
  padding: 14px 24px;
  background: var(--primary);
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  font-family: inherit;
  box-shadow: 0 2px 4px rgba(74, 144, 226, 0.15);
}

.form-submit:hover {
  background: var(--primary-dark);
  box-shadow: 0 4px 8px rgba(74, 144, 226, 0.2);
  transform: translateY(-1px);
}

.form-submit svg {
  transition: transform 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

.form-submit:hover svg {
  transform: translateX(2px);
}

@media (max-width: 768px) {
  .modal-container {
    width: 100%;
    max-width: 100%;
    border-bottom-left-radius: 0;
    border-bottom-right-radius: 0;
    max-height: 95vh;
    top: auto;
    bottom: 0;
    transform: translate(-50%, 0);
  }

  .modal-container[data-state='open'] {
    animation: contentShowMobile 250ms cubic-bezier(0.16, 1, 0.3, 1);
  }

  .modal-container[data-state='closed'] {
    animation: contentHideMobile 200ms cubic-bezier(0.16, 1, 0.3, 1);
  }

  @keyframes contentShowMobile {
    from {
      opacity: 0;
      transform: translate(-50%, 20px);
    }
    to {
      opacity: 1;
      transform: translate(-50%, 0);
    }
  }

  @keyframes contentHideMobile {
    from {
      opacity: 1;
      transform: translate(-50%, 0);
    }
    to {
      opacity: 0;
      transform: translate(-50%, 20px);
    }
  }

  .modal-header {
    padding: 24px 24px 20px;
  }

  .modal-form {
    padding: 24px;
  }

  .modal-title {
    font-size: 24px;
  }
}
</style>
