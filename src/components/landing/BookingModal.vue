<template>
  <Dialog :open="isOpen" @update:open="handleOpenChange">
    <DialogContent class="sm:max-w-[500px] p-0 gap-0 overflow-hidden bg-white">
      <div class="p-6 md:p-8 pb-5 md:pb-6 border-b border-[var(--border)]">
        <div
          class="flex items-center gap-3 p-3 bg-gradient-subtle rounded-xl mb-5 border border-[rgba(74,144,226,0.1)]"
        >
          <div
            class="w-10 h-10 rounded-lg bg-gradient-hero text-white flex items-center justify-center font-bold text-base font-[Manrope,sans-serif] shrink-0"
          >
            {{ mentorInitials }}
          </div>
          <div>
            <div class="font-semibold text-[var(--text-primary)] text-[15px]">
              {{ mentorName }}
            </div>
            <div class="text-[13px] text-[var(--primary)] font-medium">
              {{ mentorTopic }}
            </div>
          </div>
        </div>
        <DialogHeader>
          <DialogTitle
            class="text-2xl md:text-[28px] font-bold text-[var(--text-primary)] m-0 mb-2"
            >Solicitar mentoría</DialogTitle
          >
          <DialogDescription class="text-base text-[var(--text-secondary)] m-0">
            Completa tus datos y te contactaremos pronto
          </DialogDescription>
        </DialogHeader>
      </div>

      <form
        class="p-6 md:p-8 flex flex-col gap-5"
        @submit.prevent="handleSubmit"
      >
        <div class="flex flex-col gap-2">
          <Label
            for="name"
            class="text-sm font-semibold text-[var(--text-primary)]"
            >Nombre completo</Label
          >
          <Input
            id="name"
            v-model="formData.name"
            type="text"
            placeholder="Tu nombre"
            required
            class="h-auto py-3 text-[15px]"
          />
        </div>

        <div class="flex flex-col gap-2">
          <Label
            for="email"
            class="text-sm font-semibold text-[var(--text-primary)]"
            >Correo electrónico</Label
          >
          <Input
            id="email"
            v-model="formData.email"
            type="email"
            placeholder="tu@email.com"
            required
            class="h-auto py-3 text-[15px]"
          />
        </div>

        <div class="flex flex-col gap-2">
          <Label
            for="date"
            class="text-sm font-semibold text-[var(--text-primary)]"
            >Fecha preferida</Label
          >
          <Input
            id="date"
            v-model="formData.date"
            type="date"
            :min="minDate"
            required
            class="h-auto py-3 text-[15px]"
          />
        </div>

        <div class="flex flex-col gap-2">
          <Label
            for="message"
            class="text-sm font-semibold text-[var(--text-primary)]"
            >Cuéntanos sobre tus objetivos (opcional)</Label
          >
          <Textarea
            id="message"
            v-model="formData.message"
            placeholder="¿Qué te gustaría lograr con esta mentoría?"
            rows="4"
            class="resize-y min-h-[100px] text-[15px]"
          />
        </div>

        <Button
          type="submit"
          class="w-full py-6 text-base font-semibold shadow-[0_2px_4px_rgba(74,144,226,0.15)] hover:shadow-[0_4px_8px_rgba(74,144,226,0.2)]"
        >
          <span>Enviar solicitud</span>
          <svg
            class="ml-2 w-4 h-4 transition-transform duration-200 group-hover:translate-x-0.5"
            viewBox="0 0 16 16"
            fill="none"
          >
            <path
              d="M6 3L11 8L6 13"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </Button>
      </form>
    </DialogContent>
  </Dialog>
</template>

<script setup>
import { ref, computed } from "vue";
import {
  Dialog,
  DialogContent,
  DialogHeader,
  DialogTitle,
  DialogDescription,
} from "@/components/ui/dialog";
import { Input } from "@/components/ui/input";
import { Label } from "@/components/ui/label";
import { Textarea } from "@/components/ui/textarea";
import { Button } from "@/components/ui/button";

const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false,
  },
  mentorName: {
    type: String,
    default: "",
  },
  mentorTopic: {
    type: String,
    default: "",
  },
});

const emit = defineEmits(["close", "submit"]);

const formData = ref({
  name: "",
  email: "",
  date: "",
  message: "",
});

const minDate = computed(() => {
  const tomorrow = new Date();
  tomorrow.setDate(tomorrow.getDate() + 1);
  return tomorrow.toISOString().split("T")[0];
});

const mentorInitials = computed(() => {
  return props.mentorName
    .split(" ")
    .map((word) => word[0])
    .join("")
    .toUpperCase()
    .slice(0, 2);
});

const handleOpenChange = (open) => {
  if (!open) {
    emit("close");
  }
};

const handleSubmit = () => {
  console.log("Form submitted:", {
    mentor: props.mentorName,
    ...formData.value,
  });

  const params = new URLSearchParams({
    mentor: props.mentorName,
    name: formData.value.name,
    email: formData.value.email,
    date: formData.value.date,
    message: formData.value.message,
  });

  window.open(
    `https://forms.gle/JdC6fM1Fazotx6b6A?${params.toString()}`,
    "_blank"
  );

  formData.value = {
    name: "",
    email: "",
    date: "",
    message: "",
  };

  emit("close");
};
</script>
