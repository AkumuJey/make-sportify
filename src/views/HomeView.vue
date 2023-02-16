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
     <HomeCard image="https://picsum.photos/id/44/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard class="md:block hidden" image="https://picsum.photos/id/58/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard class="lg:block hidden" image="https://picsum.photos/id/69/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard class="xl:block hidden" image="https://picsum.photos/id/70/300/300" title="Title is here" subTitle="Subtital is here"/>
    </div>
  </div>
  <div class="p-8">
    <button
      type="button"
      class="text-white text-2xl font-semibold hover:underline cursor-pointer"
    >
      Recommended Radio
    </button>
    <div class="py-1.5"></div>
    <div class="flex items-center"
    >
     <HomeCard image="https://picsum.photos/id/23/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard image="https://picsum.photos/id/46/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard class="md:block hidden" image="https://picsum.photos/id/55/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard class="lg:block hidden" image="https://picsum.photos/id/66/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard class="xl:block hidden" image="https://picsum.photos/id/100/300/300" title="Title is here" subTitle="Subtital is here"/>
    </div>
  </div>
  <div class="p-8">
    <button
      type="button"
      class="text-white text-2xl font-semibold hover:underline cursor-pointer"
    >
      Recommended Songs
    </button>
    <div class="py-1.5"></div>
    <div class="flex items-center"
    >
     <HomeCard image="https://picsum.photos/id/38/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard image="https://picsum.photos/id/50/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard class="md:block hidden" image="https://picsum.photos/id/63/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard class="lg:block hidden" image="https://picsum.photos/id/72/300/300" title="Title is here" subTitle="Subtital is here"/>
     <HomeCard class="xl:block hidden" image="https://picsum.photos/id/80/300/300" title="Title is here" subTitle="Subtital is here"/>
    </div>
  </div>
</template>
