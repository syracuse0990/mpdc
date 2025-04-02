<template>
    <div class="bg-white text-white py-12 px-4 sm:px-8 md:px-32">
      <div class="max-w-screen-4xl mx-auto w-[95%]">

        <!-- News Container -->
        <div class="relative w-full overflow-hidden">
          <div class="relative group">

            <!-- Transition for Image -->
            <transition name="fade" mode="out-in">
              <img
                :key="currentIndex"
                :src="images[currentIndex].src"
                :alt="images[currentIndex].alt"
                class="w-full h-[50vh] sm:h-[60vh] md:h-[75vh] lg:h-[80vh] object-cover
                      transition-transform duration-500 transform"
              />
            </transition>

            <!-- Transition for News Content (Fade-in + Slide-up) -->
            <div
              ref="textContainer"
              class="absolute top-[50%] left-[10%] text-white font-cormorant px-4 sm:px-6 max-w-[80%] sm:max-w-[60%]
                     opacity-0 transform translate-y-10 transition-all duration-700 ease-out"
              :class="{ 'fade-in': isTextVisible }"
            >
              <h3 class="text-2xl sm:text-3xl md:text-5xl font-bold leading-tight">
                {{ images[currentIndex].title }}
              </h3>
              <p class="mt-3 text-base sm:text-lg md:text-xl lg:text-2xl leading-relaxed">
                {{ images[currentIndex].description }}
              </p>
            </div>

            <!-- Auto-Play Progress Bar -->
            <div class="absolute bottom-6 left-1/2 transform -translate-x-1/2 w-[40%]">
              <div
                class="transition-all duration-[3000ms]"
                :style="{ width: progressBarWidth }"
              ></div>
            </div>

          </div>
        </div>
      </div>
    </div>
  </template>

  <script setup lang="ts">
  import { ref, onMounted, onUnmounted } from 'vue';

  // ✅ Import images properly
import temu1 from '../images/temu1.jpg';
import temu2 from '../images/temu2.jpg';
import temu3 from '../images/temu3.jpg';

  // Array of images with correct paths and proper types
  interface Image {
    src: string;
    alt: string;
    title: string;
    description: string;
  }

  const images = ref<Image[]>([
    {
      src: temu1,
      alt: '',
      title: '',
      description: ''
    },
    {
      src: temu2,
      alt: '',
      title: '',
      description: ''
    },
    {
      src: temu3,
      alt: '',
      title: '',
      description: ''
    },
]);


  const currentIndex = ref<number>(0);
  const progressBarWidth = ref<string>('0%');
  let autoSlideInterval: NodeJS.Timeout;
  const isTextVisible = ref<boolean>(false);
  const isTitleVisible = ref<boolean>(false);
  const textContainer = ref<HTMLElement | null>(null);
  const titleContainer = ref<HTMLElement | null>(null);

  // Function to navigate to the next image
  const nextImage = (): void => {
    currentIndex.value = (currentIndex.value + 1) % images.value.length;
    resetProgress();
  };

  // Auto-slide every 3 seconds
  const startAutoSlide = (): void => {
    autoSlideInterval = setInterval(() => {
      nextImage();
    }, 5000);
  };

  // Reset progress bar
  const resetProgress = (): void => {
    progressBarWidth.value = '0%';
    setTimeout(() => {
      progressBarWidth.value = '100%';
    }, 50);
  };

  // Scroll-based fade-in effects for text & title
  const handleIntersection = (entries: IntersectionObserverEntry[]): void => {
    entries.forEach((entry) => {
      if (entry.target === textContainer.value && entry.isIntersecting) {
        isTextVisible.value = true;
      }
      if (entry.target === titleContainer.value && entry.isIntersecting) {
        isTitleVisible.value = true;
      }
    });
  };

  onMounted(() => {
    startAutoSlide();
    resetProgress();

    const observer = new IntersectionObserver(handleIntersection, { threshold: 0.6 });
    if (textContainer.value) observer.observe(textContainer.value);
    if (titleContainer.value) observer.observe(titleContainer.value);
  });

  onUnmounted(() => {
    clearInterval(autoSlideInterval);
  });
  </script>


  <style scoped>
  /* Import Custom Font */
  @import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;700&display=swap');

  .font-cormorant {
    font-family: 'Cormorant Garamond', serif;
  }

  /* Smooth Fade-in Effect */
  .fade-enter-active, .fade-leave-active {
    transition: opacity 0.8s ease-in-out;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  /* Scroll-based Text Animation */
  .opacity-0 {
    opacity: 0;
    transform: translateY(20px);
  }
  .fade-in {
    opacity: 1;
    transform: translateY(0);
  }

  /* Title Scroll Animation (Slide Down + Fade-in) */
  .fade-down {
    opacity: 1;
    transform: translateY(0);
  }
  </style>
