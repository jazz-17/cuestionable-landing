<template>
  <div class="video-thumbnail" @click="$emit('click')">
    <img
      :src="`https://img.youtube.com/vi/${videoId}/maxresdefault.jpg`"
      :alt="`Video de YouTube`"
      class="thumbnail-image"
      @error="useFallback"
    />
    <div class="play-overlay">
      <div class="play-button">
        <svg width="68" height="48" viewBox="0 0 68 48">
          <path d="M66.52,7.74c-0.78-2.93-2.49-5.41-5.42-6.19C55.79,.13,34,0,34,0S12.21,.13,6.9,1.55 C3.97,2.33,2.27,4.81,1.48,7.74C0.06,13.05,0,24,0,24s0.06,10.95,1.48,16.26c0.78,2.93,2.49,5.41,5.42,6.19 C12.21,47.87,34,48,34,48s21.79-0.13,27.1-1.55c2.93-0.78,4.64-3.26,5.42-6.19C67.94,34.95,68,24,68,24S67.94,13.05,66.52,7.74z" fill="#f00"/>
          <path d="M 45,24 27,14 27,34" fill="#fff"/>
        </svg>
      </div>
    </div>
    <div class="duration-badge">Ver video</div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  videoId: {
    type: String,
    required: true
  }
});

defineEmits(['click']);

const useFallback = (e) => {
  // If maxresdefault fails, use hqdefault
  e.target.src = `https://img.youtube.com/vi/${props.videoId}/hqdefault.jpg`;
};
</script>

<style scoped>
.video-thumbnail {
  position: relative;
  width: 100%;
  aspect-ratio: 16 / 9;
  border-radius: 12px;
  overflow: hidden;
  cursor: pointer;
  background: var(--bg-secondary);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.video-thumbnail:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
}

.video-thumbnail:hover .play-button {
  transform: scale(1.1);
}

.video-thumbnail:hover .play-overlay {
  background: rgba(0, 0, 0, 0.5);
}

.thumbnail-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.play-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.play-button {
  transition: transform 0.3s cubic-bezier(0.16, 1, 0.3, 1);
  filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.3));
}

.duration-badge {
  position: absolute;
  bottom: 12px;
  right: 12px;
  padding: 6px 12px;
  background: rgba(0, 0, 0, 0.8);
  color: white;
  font-size: 13px;
  font-weight: 600;
  border-radius: 6px;
  backdrop-filter: blur(4px);
}
</style>
