<script setup>
import CategorySelect from '../components/CategorySelect.vue'
</script>
<template>
  <div>
      <div class="p-8">
        <button
          type="button"
          class="text-white text-2xl font-semibold hover:underline cursor-pointer"
        >
          Recommended Songs
        </button>
        <div class="py-1.5"></div>
        <div class="grid xl:grid-cols-3 lg:grid-cols-4 sm:grid-cols-2 gap-6"
        >
         <CategorySelect category="Podscast" image="https://picsum.photos/id/21/300/300"/>
         <CategorySelect category="Audio Book" image="https://picsum.photos/id/11/300/300"/>
         <CategorySelect category="Surgery Talk" image="https://picsum.photos/id/15/300/300"/>
         <CategorySelect category="Hip Hop" image="https://picsum.photos/id/17/300/300"/>
         <CategorySelect category="Rhumba Nights" image="https://picsum.photos/id/19/300/300"/>
         <CategorySelect category="Ohangla" image="https://picsum.photos/id/25/300/300"/>
         <CategorySelect category="Benga" image="https://picsum.photos/id/75/300/300"/>
         <CategorySelect category="RNBS" image="https://picsum.photos/id/95/300/300"/>
         <CategorySelect category="Football Punditry" image="https://picsum.photos/id/9/300/300"/>
         <CategorySelect category="Worship" image="https://picsum.photos/id/5/300/300"/>
         <CategorySelect category="Soul" image="https://picsum.photos/id/2/300/300"/>
         <CategorySelect category="Gengetone" image="https://picsum.photos/id/1/300/300"/>
         <CategorySelect category="Dudu" image="https://picsum.photos/id/13/300/300"/>
         <CategorySelect category="Ngolo" image="https://picsum.photos/id/91/300/300"/>
         <CategorySelect category="Taarab" image="https://picsum.photos/id/93/300/300"/>
         <CategorySelect category="Bongo" image="https://picsum.photos/id/99/300/300"/>
        </div>
      </div>
  </div>
</template>

