<template>
  <div>
    <div
      v-if="videos.length > 0"
      class="grid grid-cols-1 md:grid-cols-[repeat(auto-fit,minmax(320px,1fr))] gap-8"
    >
      <div
        v-for="(videoId, index) in videos"
        :key="videoId"
        class="bg-white rounded-xl overflow-hidden border border-[var(--border)] transition-all duration-300 hover:border-[var(--primary)] hover:shadow-lg hover:-translate-y-1 reveal-on-scroll"
        :style="{ transitionDelay: `${index * 0.1}s` }"
      >
        <VideoThumbnail :videoId="videoId" @click="openVideo(videoId)" />
      </div>
    </div>

    <div
      v-else
      class="text-center py-16 px-8 bg-white rounded-2xl border border-dashed border-[var(--border)] reveal-on-scroll"
    >
      <p class="text-[var(--text-secondary)] text-lg mb-6">
        Próximamente encontrarás aquí nuestros últimos videos
      </p>
      <a
        :href="channelUrl"
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-2 px-8 py-3 bg-[var(--primary)] text-white no-underline rounded-full font-semibold transition-all duration-200 hover:bg-[var(--primary-dark)] hover:shadow-md hover:-translate-y-1"
      >
        Visitar canal
      </a>
    </div>

    <VideoModal
      :isOpen="isModalOpen"
      :videoId="currentVideoId"
      @close="closeVideo"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import VideoThumbnail from "./VideoThumbnail.vue";
import VideoModal from "./VideoModal.vue";

const props = defineProps({
  videos: {
    type: Array,
    default: () => [],
  },
  channelUrl: {
    type: String,
    required: true,
  },
});

const isModalOpen = ref(false);
const currentVideoId = ref("");

const openVideo = (videoId) => {
  currentVideoId.value = videoId;
  isModalOpen.value = true;
};

const closeVideo = () => {
  isModalOpen.value = false;
  setTimeout(() => {
    currentVideoId.value = "";
  }, 200);
};
</script>
