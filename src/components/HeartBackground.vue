<template>
  <div class="fixed inset-0 pointer-events-none overflow-hidden z-0">
    <div
      v-for="heart in hearts"
      :key="heart.id"
      class="absolute text-love-pink opacity-20 animate-float"
      :style="{
        left: heart.left + '%',
        top: heart.top + '%',
        fontSize: heart.size + 'rem',
        animationDuration: heart.duration + 's',
        animationDelay: heart.delay + 's',
      }"
    >
      ❤
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const hearts = ref([]);

onMounted(() => {
  for (let i = 0; i < 20; i++) {
    hearts.value.push({
      id: i,
      left: Math.random() * 100,
      top: Math.random() * 100,
      size: 0.5 + Math.random() * 2,
      duration: 3 + Math.random() * 7,
      delay: Math.random() * 5,
    });
  }
});
</script>
