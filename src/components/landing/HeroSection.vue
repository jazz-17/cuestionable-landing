<template>
  <section
    class="hero relative py-20 pt-[140px] md:py-24 md:pt-32 overflow-hidden bg-gradient-hero"
  >
    <div class="container relative z-10">
      <div class="max-w-[800px] mx-auto text-center">
        <div
          class="inline-flex items-center gap-2 px-4 py-2 bg-[rgba(158,191,166,0.1)] border border-[rgba(158,191,166,0.2)] rounded-full text-sm font-medium text-[var(--primary-dark)] mb-8 animate-fade-in"
        >
          <span class="relative flex h-2 w-2">
            <span
              class="animate-ping absolute inline-flex h-full w-full rounded-full bg-[var(--primary)] opacity-75"
            ></span>
            <span
              class="relative inline-flex rounded-full h-2 w-2 bg-[var(--primary)]"
            ></span>
          </span>
          <span>Mentorías personalizadas 1 a 1</span>
        </div>

        <h1
          class="text-5xl md:text-[64px] font-bold text-[var(--text-primary)] mb-6 leading-[1.1] tracking-tight animate-fade-in"
          style="animation-delay: 0.1s"
        >
          Potencia tu carrera con <br />
          <span class="text-[var(--primary)]">mentores expertos</span>
        </h1>

        <p
          class="text-lg md:text-xl leading-relaxed text-[var(--text-secondary)] mb-10 max-w-2xl mx-auto animate-fade-in"
          style="animation-delay: 0.2s"
        >
          Conecta con profesionales en Business Intelligence y desarrollo
          profesional. Sesiones diseñadas para alcanzar tus objetivos.
        </p>

        <div
          class="flex justify-center gap-4 flex-col sm:flex-row animate-fade-in"
          style="animation-delay: 0.3s"
        >
          <a
            :href="formUrl"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center justify-center gap-2 px-8 py-4 bg-[var(--primary)] text-white no-underline rounded-full font-semibold text-lg transition-all duration-300 hover:bg-[var(--primary-dark)] hover:shadow-lg hover:-translate-y-1"
          >
            <span>Solicitar mentoría</span>
            <svg
              width="20"
              height="20"
              viewBox="0 0 20 20"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M5 12h14"></path>
              <path d="M12 5l7 7-7 7"></path>
            </svg>
          </a>
          <a
            href="#como-funciona"
            class="inline-flex items-center justify-center gap-2 px-8 py-4 bg-white text-[var(--text-primary)] no-underline rounded-full font-semibold text-lg border border-[var(--border)] transition-all duration-300 hover:bg-[var(--bg-secondary)] hover:border-[var(--primary)] hover:text-[var(--primary)]"
          >
            Cómo funciona
          </a>
        </div>
      </div>
    </div>

    <!-- Decorative elements -->
    <div
      class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[800px] h-[800px] bg-[var(--primary)] opacity-[0.03] rounded-full blur-3xl pointer-events-none -z-1"
    ></div>
  </section>
</template>

<script setup>
defineProps({
  formUrl: {
    type: String,
    required: true,
  },
});
</script>
