<template>
  <div
    class="relative min-h-screen font-sans selection:bg-love-pink selection:text-white"
  >
    <HeartBackground />

    <main class="relative z-10">
      <HeroSection />
      <StorySection />
      <LoveQuiz @complete="isQuizFinished = true" />

      <Transition
        enter-active-class="transition-all duration-1000 ease-out"
        enter-from-class="opacity-0 translate-y-20"
        enter-to-class="opacity-100 translate-y-0"
      >
        <LoveQuest v-if="isQuizFinished" @complete="isQuestFinished = true" />
      </Transition>

      <Transition
        enter-active-class="transition-all duration-1000 ease-out"
        enter-from-class="opacity-0 translate-y-20"
        enter-to-class="opacity-100 translate-y-0"
      >
        <InteractiveWish v-if="isQuestFinished" />
      </Transition>
    </main>

    <footer class="py-10 text-center text-love-deep opacity-60">
      <p>© 2026 Made with ❤️ for someone special</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from "vue";
import HeartBackground from "./components/HeartBackground.vue";
import HeroSection from "./components/HeroSection.vue";
import InteractiveWish from "./components/InteractiveWish.vue";
import LoveQuest from "./components/LoveQuest.vue";
import LoveQuiz from "./components/LoveQuiz.vue";
import StorySection from "./components/StorySection.vue";

const isQuizFinished = ref(false);
const isQuestFinished = ref(false);
</script>
