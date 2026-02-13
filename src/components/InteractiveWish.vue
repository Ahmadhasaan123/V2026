<template>
  <section
    id="ask"
    class="min-h-screen flex flex-col items-center justify-center px-6 text-center relative overflow-hidden"
  >
    <div v-if="!accepted" class="space-y-10">
      <h2 class="text-4xl md:text-6xl font-black text-love-dark leading-tight">
        Will You Be My <br /><span
          class="text-love-deep italic underline decoration-love-pink"
          >Valentine?</span
        >
      </h2>

      <div class="flex flex-col md:flex-row items-center justify-center gap-6">
        <button
          @click="accept"
          class="bg-love-deep text-white px-12 py-4 rounded-full text-2xl font-bold shadow-xl hover:scale-110 active:scale-95 transition-all w-48"
        >
          Yes! 💖
        </button>

        <button
          @mouseover="moveNoButton"
          @touchstart="moveNoButton"
          :style="noButtonStyle"
          class="bg-gray-200 text-gray-500 px-12 py-4 rounded-full text-2xl font-bold transition-all duration-200 w-48 md:static absolute"
        >
          No... 🥺
        </button>
      </div>
    </div>

    <div v-else class="space-y-8 animate-in zoom-in duration-1000 max-w-2xl">
      <h2 class="text-5xl md:text-7xl font-black text-love-deep">YES! ❤️</h2>

      <div
        class="p-8 bg-white/40 backdrop-blur-md rounded-3xl border border-white/20 shadow-2xl relative"
      >
        <span
          class="absolute -top-6 -left-4 text-6xl text-love-pink opacity-50 italic font-serif"
          >"</span
        >
        <p
          class="text-2xl md:text-3xl text-love-dark font-serif italic leading-relaxed"
        >
          Stay mine , forever
        </p>
        <span class="block mt-4 text-xl font-bold text-love-deep"
          >— Belonta</span
        >
        <span
          class="absolute -bottom-10 -right-4 text-6xl text-love-pink opacity-50 italic font-serif"
          >"</span
        >
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";

const accepted = ref(false);
const noButtonStyle = ref({});

const accept = () => {
  accepted.value = true;
};

const moveNoButton = () => {
  const x = Math.random() * (window.innerWidth - 150);
  const y = Math.random() * (window.innerHeight - 100);
  noButtonStyle.value = {
    position: "absolute",
    left: `${x}px`,
    top: `${y}px`,
    zIndex: 50,
  };
};
</script>
