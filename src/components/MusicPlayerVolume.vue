<script setup>
import { ref, onMounted } from 'vue'

// Import of components
import VolumeMute from 'vue-material-design-icons/VolumeMute.vue'
import VolumeHigh from 'vue-material-design-icons/VolumeHigh.vue'



// Store components
import { useSongStore } from '../stores/song'
import { storeToRefs } from "pinia";

const useSong = useSongStore()

const { audio } = storeToRefs(useSong)
let isHover = ref(false)
let vol = ref(80)
let volume = ref(null)


// Volume functionality
onMounted(() => {
    volume.value.addEventListener("input",(e) => {
        audio.value.volume = e.currentTarget.value / 100
    })
})

</script>
<template>
  <VolumeMute v-if="vol == 0" class="text-white" :size="20"/>
  <VolumeHigh v-else class="text-white" :size="20"/>
  <div
    class="flex items-center ml-2 w-40 relative mt-2 mb-6"
    @mouseenter="isHover = true"
    @mouseleave="isHover = false"
   >
        <input
            type="range"
            v-model="vol"
            ref="volume"
            class="absolute rounded-full my-2 mt-6 w-full h-0 z-40 appearance-none bg-opacity-100 focus:outline-none accent-white"
            :class="{'rangeDotHidden': !isHover}"
                >
        <div
            class="pointer-events-none mt-1.5 absolute h-1 z-10 inset-y-0 left-0 w-0"
            :style="`width:${vol}%;`"
            :class="[isHover ? 'bg-green-500' : 'bg-white']"
        />
        <div class="absolute h-1 -z-0 mt-1.5 inset-y-0 left-0 w-full bg-gray-500 rounded-full"></div>
    </div>
</template>


<style>

</style>