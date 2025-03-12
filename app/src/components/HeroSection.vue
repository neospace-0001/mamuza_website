<template>
  <section class="relative bg-orange-50 py-12">
    <div class="container mx-auto max-w-7xl">
      <div class="carousel-container overflow-hidden relative">
        <button
          @click="prevSlide"
          class="absolute left-0 top-1/2 transform -translate-y-1/2 bg-gray-200 hover:bg-gray-300 text-gray-700 font-bold py-2 px-4 rounded-r focus:outline-none focus:shadow-outline z-10"
        >
          Previous
        </button>

        <div
          class="carousel-slide flex transition-transform duration-500"
          :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
        >
          <div
            v-for="(item, index) in carouselItems"
            :key="index"
            class="carousel-item w-full flex-shrink-0 p-4"
          >
            <div class="flex items-center md:h-[60vh]">
              <div
                class="w-full h-full bg-cover bg-center rounded-lg relative"
                :style="{ backgroundImage: `url(${item.image})` }"
                :aria-label="item.alt"
                role="img"
              >
                <!-- Content Overlay -->
                <div
                  class="absolute top-0 left-0 w-full h-full p-4 flex flex-col justify-end items-center bg-gray-500/80  text-white"
                >
                  <h2 class="text-2xl font-semibold">{{ item.title }}</h2>
                  <p class="mt-2">{{ item.description }}</p>
                  <button
                    class="mt-4 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                  >
                    Learn More
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <button
          @click="nextSlide"
          class="absolute right-0 top-1/2 transform -translate-y-1/2 bg-gray-200 hover:bg-gray-300 text-gray-700 font-bold py-2 px-4 rounded-l focus:outline-none focus:shadow-outline"
        >
          Next
        </button>
      </div>

      <div class="carousel-controls mt-4 flex justify-center items-center">
        <button
          v-for="(item, index) in carouselItems"
          :key="index"
          @click="goToSlide(index)"
          class="h-3 w-3 rounded-full mx-3"
          :class="{
            'bg-blue-500': currentIndex === index,
            'bg-gray-300 hover:bg-gray-400': currentIndex !== index,
          }"
        ></button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const carouselItems = ref([
  {
    image: "../src/assets/media/hero.jpg",
    alt: "Image 1",
    title: "EdTech",
    description:
      "Item 1 Description: This is some example text for the first carousel item.",
  },
  {
    image: "../src/assets/media/hero1.jpg",
    alt: "Image 2",
    title: "Software",
    description:
      "Item 2 Description: This is some example text for the second carousel item.",
  },
  {
    image: "../src/assets/media/hero2.jpg",
    alt: "Image 3",
    title: "engineering",
    description:
      "Item 3 Description: This is some example text for the third carousel item.",
  },
  {
    image: "../src/assets/media/hero1.jpg",
    alt: "Image 2",
    title: "Software",
    description:
      "Item 2 Description: This is some example text for the second carousel item.",
  },
  {
    image: "../src/assets/media/hero2.jpg",
    alt: "Image 3",
    title: "engineering",
    description:
      "Item 3 Description: This is some example text for the third carousel item.",
  },
]);

const currentIndex = ref(0);
let intervalId;

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % carouselItems.value.length;
};

const prevSlide = () => {
  currentIndex.value =
    (currentIndex.value - 1 + carouselItems.value.length) %
    carouselItems.value.length;
};

const goToSlide = (index) => {
  currentIndex.value = index;
};

onMounted(() => {
  intervalId = setInterval(nextSlide, 3000);
});

onUnmounted(() => {
  clearInterval(intervalId);
});
</script>

<style scoped>
@keyframes slideInFromRight {
  0% {
    transform: translateX(100%);
    opacity: 0;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}
</style>
