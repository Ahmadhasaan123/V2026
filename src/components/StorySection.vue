<template>
  <section
    id="story"
    class="min-h-screen flex flex-col items-center justify-center px-6 py-20 space-y-12"
  >
    <h2 class="text-3xl md:text-5xl font-bold text-love-dark">Our Moments</h2>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 max-w-4xl w-full">
      <div
        v-for="(memory, index) in memories"
        :key="index"
        class="bg-white/40 backdrop-blur-md p-6 rounded-3xl border border-white/20 shadow-xl transform transition-all hover:rotate-2"
      >
        <div class="text-4xl mb-4">{{ memory.emoji }}</div>
        <h3 class="text-xl font-bold text-love-dark mb-2">
          {{ memory.title }}
        </h3>
        <p class="text-love-deep/80">{{ memory.desc }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
const memories = [
  {
    emoji: "✨",
    title: "The Spark",
    desc: "That first moment we connected, and I knew you were special.",
  },
  {
    emoji: "🌙",
    title: "Late Night Talks",
    desc: "When hours felt like minutes and every word mattered.",
  },
  {
    emoji: "🍦",
    title: "Sweet Adventures",
    desc: "All the little dates that made life taste better.",
  },
  {
    emoji: "🫂",
    title: "Safe Place",
    desc: "Finding home in your arms and peace in your smile.",
  },
];
</script>
