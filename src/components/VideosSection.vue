<template>
  <div>
    <div v-if="videos.length > 0" class="videos-grid">
      <div
        v-for="videoId in videos"
        :key="videoId"
        class="video-card"
      >
        <VideoThumbnail :videoId="videoId" @click="openVideo(videoId)" />
      </div>
    </div>

    <div v-else class="no-videos">
      <p>Próximamente encontrarás aquí nuestros últimos videos</p>
      <a :href="channelUrl" target="_blank" rel="noopener noreferrer" class="visit-channel">
        Visitar canal
      </a>
    </div>

    <VideoModal :isOpen="isModalOpen" :videoId="currentVideoId" @close="closeVideo" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import VideoThumbnail from './VideoThumbnail.vue';
import VideoModal from './VideoModal.vue';

const props = defineProps({
  videos: {
    type: Array,
    default: () => []
  },
  channelUrl: {
    type: String,
    required: true
  }
});

const isModalOpen = ref(false);
const currentVideoId = ref('');

const openVideo = (videoId) => {
  currentVideoId.value = videoId;
  isModalOpen.value = true;
};

const closeVideo = () => {
  isModalOpen.value = false;
  // Delay clearing the video ID to allow modal to close smoothly
  setTimeout(() => {
    currentVideoId.value = '';
  }, 200);
};
</script>

<style scoped>
/* Grid styles moved from index.astro */
.videos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 24px;
}

.video-card {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid var(--border);
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}

.video-card:hover {
  border-color: rgba(74, 144, 226, 0.2);
}

.no-videos {
  text-align: center;
  padding: 60px 32px;
  background: white;
  border-radius: 16px;
  border: 2px dashed var(--border);
}

.no-videos p {
  color: var(--text-secondary);
  font-size: 16px;
  margin-bottom: 20px;
}

.visit-channel {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 24px;
  background: var(--gradient-hero);
  color: white;
  text-decoration: none;
  border-radius: 8px;
  font-weight: 600;
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
  box-shadow: 0 2px 4px rgba(74, 144, 226, 0.15);
}

.visit-channel:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 8px rgba(74, 144, 226, 0.2);
}

@media (max-width: 768px) {
  .videos-grid {
    grid-template-columns: 1fr;
  }
}
</style>
