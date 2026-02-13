<template>
  <section
    id="quest"
    class="min-h-screen flex flex-col items-center justify-center px-6 py-20 relative overflow-hidden bg-white/30 backdrop-blur-sm"
  >
    <div class="max-w-xl w-full">
      <!-- Step 1: Love Meter -->
      <div
        v-if="currentStep === 1"
        class="space-y-8 animate-in fade-in slide-in-from-bottom-5 duration-700 text-center"
      >
        <h2 class="text-3xl md:text-5xl font-bold text-love-dark">
          How much do you love me? 🥺
        </h2>
        <div class="relative pt-10">
          <input
            type="range"
            v-model="loveValue"
            min="0"
            max="100"
            class="w-full h-4 bg-love-pale rounded-lg appearance-none cursor-pointer accent-love-deep"
          />
          <div
            class="mt-8 text-6xl transform transition-transform duration-300"
            :style="{ scale: 1 + loveValue / 100 }"
          >
            {{ loveValue > 80 ? "💖" : loveValue > 40 ? "😊" : "🧐" }}
          </div>
          <p class="mt-4 text-love-deep font-bold text-2xl">
            {{ loveValue }}% and counting...
          </p>
        </div>
        <button
          v-if="loveValue > 90"
          @click="nextStep"
          class="bg-love-deep text-white px-10 py-3 rounded-full font-bold shadow-lg hover:bg-love-dark transition-colors"
        >
          Next Challenge ✨
        </button>
        <p v-else class="text-sm text-love-dark/60">
          Must be at least 90% for the next step! 😉
        </p>
      </div>

      <!-- Step 2: Secret Message Catcher -->
      <div
        v-if="currentStep === 2"
        class="space-y-8 animate-in fade-in slide-in-from-bottom-5 duration-700 text-center"
      >
        <h2 class="text-3xl md:text-5xl font-bold text-love-dark">
          Catch my heart!
        </h2>
        <p class="text-love-deep">Tap the heart to reveal a secret...</p>
        <div
          class="relative h-64 bg-love-pale/30 rounded-3xl border-2 border-dashed border-love-pink/50 flex items-center justify-center"
        >
          <button
            @click="catchHeart"
            @touchstart.passive="moveHeart"
            @mousedown="moveHeart"
            :style="heartPos"
            class="text-5xl absolute transition-all duration-200 cursor-pointer hover:scale-125"
          >
            ❤️
          </button>
          <div
            v-if="heartCaught"
            class="bg-white p-6 rounded-2xl shadow-xl animate-bounce"
          >
            <p class="text-xl font-bold text-love-dark italic">
              "Every heart beat of mine belongs to you."
            </p>
          </div>
        </div>
        <button
          v-if="heartCaught"
          @click="nextStep"
          class="bg-love-deep text-white px-10 py-3 rounded-full font-bold shadow-lg"
        >
          One Last Step 🌸
        </button>
      </div>

      <!-- Step 3: Bouquet Builder -->
      <div
        v-if="currentStep === 3"
        class="space-y-8 animate-in fade-in slide-in-from-bottom-5 duration-700 text-center"
      >
        <h2 class="text-3xl md:text-5xl font-bold text-love-dark">
          A Bouquet for You
        </h2>
        <p class="text-love-deep">Tap flowers to build your dream bouquet!</p>

        <div class="flex justify-center gap-4 text-4xl mb-8">
          <button
            v-for="f in ['🌹', '🌸', '💐', '🌻', '🌷']"
            :key="f"
            @click="addFlower(f)"
            class="hover:scale-125 transition-transform"
          >
            {{ f }}
          </button>
        </div>

        <div
          class="min-h-[100px] flex flex-wrap justify-center gap-2 p-6 bg-white/50 rounded-3xl"
        >
          <span
            v-for="(f, i) in bouquet"
            :key="i"
            class="text-4xl animate-in zoom-in duration-300"
            >{{ f }}</span
          >
          <p v-if="bouquet.length === 0" class="text-love-dark/40 italic">
            Your bouquet is empty...
          </p>
        </div>

        <button
          v-if="bouquet.length >= 5"
          @click="finishQuest"
          class="bg-love-deep text-white px-10 py-4 rounded-full text-xl font-bold shadow-xl animate-pulse"
        >
          I'm Ready for the Question 🌹
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(["complete"]);
const currentStep = ref(1);
const loveValue = ref(50);
const heartCaught = ref(false);
const heartPos = ref({ top: "50%", left: "50%" });
const bouquet = ref([]);

const nextStep = () => {
  currentStep.value++;
};

const catchHeart = () => {
  if (heartCaught.value) return;
  heartCaught.value = true;
};

const moveHeart = () => {
  if (heartCaught.value) return;
  const top = 10 + Math.random() * 80;
  const left = 10 + Math.random() * 80;
  heartPos.value = { top: `${top}%`, left: `${left}%` };
};

// Move heart periodically until caught
const heartInterval = setInterval(() => {
  if (!heartCaught.value) moveHeart();
}, 800);

const addFlower = (flower) => {
  if (bouquet.value.length < 12) {
    bouquet.value.push(flower);
  }
};

const finishQuest = () => {
  emit("complete");
  document.getElementById("ask").scrollIntoView({ behavior: "smooth" });
};
</script>

<style scoped>
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  border: 4px solid #fff;
  height: 24px;
  width: 24px;
  border-radius: 50%;
  background: #ff4d6d;
  cursor: pointer;
  box-shadow: 0 0 10px rgba(255, 77, 109, 0.5);
}
</style>
