<template>
  <div class="relative w-full aspect-video rounded-xl overflow-hidden cursor-pointer bg-[var(--bg-secondary)] transition-all duration-300 transition-smooth hover:-translate-y-1 hover:shadow-[0_20px_40px_rgba(0,0,0,0.15)] group" @click="$emit('click')">
    <img
      :src="`https://img.youtube.com/vi/${videoId}/maxresdefault.jpg`"
      :alt="`Video de YouTube`"
      class="w-full h-full object-cover block"
      @error="useFallback"
    />
    <div class="absolute inset-0 bg-black/30 flex items-center justify-center transition-all duration-300 transition-smooth group-hover:bg-black/50">
      <div class="transition-transform duration-300 transition-smooth drop-shadow-[0_4px_8px_rgba(0,0,0,0.3)] group-hover:scale-110">
        <svg width="68" height="48" viewBox="0 0 68 48">
          <path d="M66.52,7.74c-0.78-2.93-2.49-5.41-5.42-6.19C55.79,.13,34,0,34,0S12.21,.13,6.9,1.55 C3.97,2.33,2.27,4.81,1.48,7.74C0.06,13.05,0,24,0,24s0.06,10.95,1.48,16.26c0.78,2.93,2.49,5.41,5.42,6.19 C12.21,47.87,34,48,34,48s21.79-0.13,27.1-1.55c2.93-0.78,4.64-3.26,5.42-6.19C67.94,34.95,68,24,68,24S67.94,13.05,66.52,7.74z" fill="#f00"/>
          <path d="M 45,24 27,14 27,34" fill="#fff"/>
        </svg>
      </div>
    </div>
    <div class="absolute bottom-3 right-3 px-3 py-1.5 bg-black/80 text-white text-[13px] font-semibold rounded-md backdrop-blur-sm">Ver video</div>
  </div>
</template>

<script setup>
const props = defineProps({
  videoId: {
    type: String,
    required: true
  }
});

defineEmits(['click']);

const useFallback = (e) => {
  e.target.src = `https://img.youtube.com/vi/${props.videoId}/hqdefault.jpg`;
};
</script>
