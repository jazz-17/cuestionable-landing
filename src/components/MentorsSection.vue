<template>
  <div class="mentors-grid">
    <MentorCard
      v-for="(mentor, index) in mentors"
      :key="index"
      :name="mentor.name"
      :topic="mentor.topic"
      :availability="mentor.availability"
      :rating="mentor.rating"
      :image="mentor.image"
      :bio="mentor.bio"
      button-text="Solicitar mentoría"
      @book="openBookingModal"
      @show-bio="openBioModal"
    />
  </div>

  <BookingModal
    :is-open="isBookingModalOpen"
    :mentor-name="selectedMentor.name"
    :mentor-topic="selectedMentor.topic"
    @close="closeBookingModal"
  />

  <MentorBioModal
    :is-open="isBioModalOpen"
    :mentor-name="selectedBio.name"
    :mentor-topic="selectedBio.topic"
    :mentor-bio="selectedBio.bio"
    :mentor-image="selectedBio.image"
    :mentor-rating="selectedBio.rating"
    @close="closeBioModal"
  />
</template>

<script setup>
import { ref } from 'vue';
import MentorCard from './MentorCard.vue';
import BookingModal from './BookingModal.vue';
import MentorBioModal from './MentorBioModal.vue';

defineProps({
  mentors: {
    type: Array,
    required: true
  }
});

const isBookingModalOpen = ref(false);
const isBioModalOpen = ref(false);

const selectedMentor = ref({
  name: '',
  topic: ''
});

const selectedBio = ref({
  name: '',
  topic: '',
  bio: '',
  image: '',
  rating: 0
});

const openBookingModal = (mentorData) => {
  selectedMentor.value = mentorData;
  isBookingModalOpen.value = true;
};

const closeBookingModal = () => {
  isBookingModalOpen.value = false;
};

const openBioModal = (bioData) => {
  selectedBio.value = bioData;
  isBioModalOpen.value = true;
};

const closeBioModal = () => {
  isBioModalOpen.value = false;
};
</script>

<style scoped>
.mentors-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 32px;
  max-width: 1000px;
  margin: 0 auto;
}

@media (max-width: 768px) {
  .mentors-grid {
    grid-template-columns: 1fr;
  }
}
</style>
