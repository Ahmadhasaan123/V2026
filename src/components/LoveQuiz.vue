<template>
  <section
    id="quiz"
    class="min-h-screen flex flex-col items-center justify-center px-6 py-20 bg-white/40 backdrop-blur-md relative overflow-hidden"
  >
    <div class="max-w-xl w-full">
      <h2
        class="text-3xl md:text-5xl font-bold text-love-dark text-center mb-12"
      >
        The "Us" Quiz 🧩
      </h2>

      <div
        v-if="!quizFinished"
        class="space-y-8 animate-in fade-in slide-in-from-bottom-5 duration-700"
      >
        <!-- Question Indicator -->
        <div class="flex justify-center gap-2 mb-6">
          <div
            v-for="i in quizQuestions.length"
            :key="i"
            class="h-2 w-8 rounded-full transition-colors duration-300"
            :class="
              i <= currentQuestionIndex + 1 ? 'bg-love-deep' : 'bg-love-pink/30'
            "
          ></div>
        </div>

        <!-- Question Content -->
        <div
          class="bg-white/80 p-8 rounded-3xl shadow-xl border border-love-pink/20"
        >
          <p class="text-2xl font-bold text-love-dark mb-6">
            {{ currentQuestion.text }}
          </p>

          <div
            v-if="currentQuestion.type === 'mcq'"
            class="grid grid-cols-1 gap-4"
          >
            <button
              v-for="(option, index) in currentQuestion.options"
              :key="index"
              @click="handleAnswer(index)"
              class="w-full text-left p-4 rounded-2xl border-2 border-love-pink/20 hover:border-love-deep hover:bg-love-pale transition-all font-medium text-love-dark group"
            >
              <span
                class="inline-block w-8 h-8 rounded-full bg-love-pink/10 text-center mr-3 group-hover:bg-love-deep group-hover:text-white transition-colors"
              >
                {{ String.fromCharCode(65 + index) }}
              </span>
              {{ option }}
            </button>
          </div>
        </div>
      </div>

      <!-- Quiz Results -->
      <div v-else class="text-center space-y-8 animate-in zoom-in duration-700">
        <div class="text-6xl mb-4">🏆</div>
        <h3 class="text-4xl font-bold text-love-dark">Quiz Complete!</h3>
        <p class="text-xl text-love-deep font-medium italic">
          "Every answer brought us closer. {{ score }} /
          {{ quizQuestions.length }} correct, 100% in my heart."
        </p>
        <button
          @click="finish"
          class="bg-love-deep text-white px-12 py-4 rounded-full text-xl font-bold shadow-pink-500/50 shadow-xl hover:scale-105 transition-transform"
        >
          Begin the Quest ⚔️
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed, ref } from "vue";

const emit = defineEmits(["complete"]);

const quizQuestions = [
  {
    text: "What was the first song i sang for you? ",
    type: "mcq",
    options: [
      "Abhi na jao chor kar",
      "Chalo dur kahin",
      "Mayi Rii",
      "Bary achy lagty hn",
    ],
    correct: "Mayi Rii",
  },
  {
    text: "What was the first compliment i ever gave you?",
    type: "mcq",
    options: ["About Your eyes", "Your Heart", "Your Lipstick", "Your Voice"],
    correct: "Your Lipstick",
  },
  {
    text: "What's my absolute favorite thing about you?",
    type: "mcq",
    options: [
      "Your smile",
      "Your Heart",
      "Your Gussa",
      "Everything (Full packet)",
    ],
    correct: "Everything (Full packet)",
  },
  {
    text: "If we were emojis, which pair would we be?",
    type: "mcq",
    options: ["🍕 & 🥤", "🌙 & ⭐", "🐱 & 🐶", "👩❤️👨"],
    correct: "👩❤️👨",
  },
  {
    text: "What's our ideal date setting?",
    type: "mcq",
    options: ["Sunset beach", "Movie night", "Jail", "Fancy dinner"],
    correct: "Fancy dinner",
  },
  {
    text: "How much space do you take in my mind?",
    type: "mcq",
    options: ["50%", "80%", "99%", "Rent-free 24/7"],
    correct: "Rent-free 24/7",
  },
];

const currentQuestionIndex = ref(0);
const score = ref(0);
const quizFinished = ref(false);

const currentQuestion = computed(
  () => quizQuestions[currentQuestionIndex.value],
);

const handleAnswer = (choiceIndex) => {
  const selectedOption = currentQuestion.value.options[choiceIndex];
  if (currentQuestion.value.type === "mcq") {
    if (selectedOption === currentQuestion.value.correct) {
      score.value++;
    }
  }

  if (currentQuestionIndex.value < quizQuestions.length - 1) {
    currentQuestionIndex.value++;
  } else {
    quizFinished.value = true;
  }
};

const finish = () => {
  emit("complete");
  const questEl = document.getElementById("quest");
  if (questEl) {
    questEl.scrollIntoView({ behavior: "smooth" });
  }
};
</script>
