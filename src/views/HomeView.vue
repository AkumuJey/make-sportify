<script setup>
import HomeCard from '../components/HomeCard.vue'


</script>

<template>
  <div class="p-8">
    <button
      type="button"
      class="text-white text-2xl font-semibold hover:underline cursor-pointer"
    >
      Podcasts to make you smatter
    </button>
    <div class="py-1.5"></div>
    <div class="flex items-center"
    >
     <HomeCard image="https://picsum.photos/id/30/300/300" title="Title is here" subTitle="Subtital is here"/>
    </div>
  </div>
</template>
