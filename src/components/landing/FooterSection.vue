<template>
  <footer class="bg-[var(--text-primary)] text-white py-15 pb-8">
    <div class="container">
      <div
        class="grid grid-cols-1 md:grid-cols-[1.5fr_1fr] gap-8 md:gap-12 pb-8 border-b border-white/10"
      >
        <div>
          <div class="flex items-center gap-2 mb-3">
            <img
              src="/logo.png"
              alt="CuestionaBle Logo"
              class="h-8 w-8 object-contain rounded-lg bg-white p-0.5"
            />
            <h3 class="text-lg font-bold m-0">CuestionaBle Mentorship</h3>
          </div>
          <p class="text-[15px] leading-relaxed opacity-70 max-w-[400px]">
            Hecho con intención para que cuestiones, aprendas y crezcas.
          </p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 md:gap-8">
          <div>
            <h4
              class="text-[13px] font-semibold mb-3 uppercase tracking-wide opacity-50"
            >
              Navegación
            </h4>
            <ul class="list-none flex flex-col gap-2.5">
              <li>
                <a
                  href="#como-funciona"
                  class="text-white no-underline opacity-80 hover:opacity-100 transition-opacity duration-200 text-sm"
                  >Cómo funciona</a
                >
              </li>
              <li>
                <a
                  href="#mentores"
                  class="text-white no-underline opacity-80 hover:opacity-100 transition-opacity duration-200 text-sm"
                  >Mentores</a
                >
              </li>
              <li>
                <a
                  href="#faq"
                  class="text-white no-underline opacity-80 hover:opacity-100 transition-opacity duration-200 text-sm"
                  >FAQ</a
                >
              </li>
            </ul>
          </div>

          <div>
            <h4
              class="text-[13px] font-semibold mb-3 uppercase tracking-wide opacity-50"
            >
              Contacto
            </h4>
            <ul class="list-none flex flex-col gap-2.5">
              <li>
                <a
                  href="mailto:contacto@cuestionable.pe"
                  class="text-white no-underline opacity-80 hover:opacity-100 transition-opacity duration-200 text-sm"
                  >contacto@cuestionable.pe</a
                >
              </li>
            </ul>
          </div>
        </div>
      </div>

      <div class="text-center pt-6 text-sm opacity-60">
        <p>&copy; {{ new Date().getFullYear() }} CuestionaBle Mentorship</p>
      </div>
    </div>
  </footer>
</template>
