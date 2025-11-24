<template>
  <div>
    <div v-if="videos.length > 0" class="grid grid-cols-1 md:grid-cols-[repeat(auto-fit,minmax(320px,1fr))] gap-6">
      <div
        v-for="videoId in videos"
        :key="videoId"
        class="bg-white rounded-xl overflow-hidden border border-[var(--border)] transition-all duration-300 transition-smooth hover:border-[rgba(74,144,226,0.2)]"
      >
        <VideoThumbnail :videoId="videoId" @click="openVideo(videoId)" />
      </div>
    </div>

    <div v-else class="text-center py-15 px-8 bg-white rounded-2xl border-2 border-dashed border-[var(--border)]">
      <p class="text-[var(--text-secondary)] text-base mb-5">Próximamente encontrarás aquí nuestros últimos videos</p>
      <a :href="channelUrl" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-2 px-6 py-3 bg-gradient-hero text-white no-underline rounded-lg font-semibold transition-all duration-200 transition-smooth shadow-[0_2px_4px_rgba(74,144,226,0.15)] hover:-translate-y-[1px] hover:shadow-[0_4px_8px_rgba(74,144,226,0.2)]">
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
  setTimeout(() => {
    currentVideoId.value = '';
  }, 200);
};
</script>
