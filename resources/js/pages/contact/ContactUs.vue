<template>
    <AppLayout>
    <div>
      <!-- Hero Image -->
      <div
        class="w-full h-[50vh] sm:h-[65vh] md:h-[75vh] lg:h-[90vh] xl:h-screen bg-cover bg-center relative"
        :style="{ backgroundImage: `url(${heroImage})` }"
      >
        <!-- Add an overlay if needed -->
        <div class="absolute inset-0 bg-black/30"></div>
      </div>

      <!-- Add margin or padding to separate from the image -->
      <div class="bg-white">
        <ContactUs1 />

      </div>
    </div>
</AppLayout>
  </template>



<script setup lang="ts">
import { ref, onMounted } from 'vue';
import AppLayout from '@/layouts/AppLayout.vue';
import heroImage from '../../images/contactimage.jpg';
import ContactUs1 from './ContactUs1.vue';

const isImageVisible = ref(false);
const isTextVisible = ref(false);
const imageContainer = ref<HTMLElement | null>(null);
const textContainer = ref<HTMLElement | null>(null);

// Intersection Observer for smooth fade-in when scrolling
const handleIntersection = (entries: IntersectionObserverEntry[]) => {
    entries.forEach((entry) => {
        if (entry.isIntersecting) {
            if (entry.target === imageContainer.value) {
                isImageVisible.value = true;
            }
            if (entry.target === textContainer.value) {
                isTextVisible.value = true;
            }
        }
    });
};

onMounted(() => {
    const observer = new IntersectionObserver(handleIntersection, { threshold: 0.3 });

    if (imageContainer.value) observer.observe(imageContainer.value);
    if (textContainer.value) observer.observe(textContainer.value);
});
</script>


<style scoped>
/* Import Custom Font */
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;700&display=swap');

.font-cormorant {
    font-family: 'Cormorant Garamond', serif;
}

/* Initial State */
.opacity-0 {
    opacity: 0;
    transform: translateY(20px);
}

/* Fade-in on Scroll */
.fade-in {
    opacity: 1;
    transform: translateY(0);
}
</style>
