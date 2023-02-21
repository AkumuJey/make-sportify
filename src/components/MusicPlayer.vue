<script setup>
// Vue imports
import { onMounted, ref, watch } from 'vue'

import MusicPlayerVolume from '../components/MusicPlayerVolume.vue'

import Heart from 'vue-material-design-icons/Heart.vue'
import PictureInPictureBottomRight from 'vue-material-design-icons/PictureInPictureBottomRight.vue'
import Play from 'vue-material-design-icons/Play.vue'
import Pause from 'vue-material-design-icons/Pause.vue'
import SkipFoward from 'vue-material-design-icons/SkipForward.vue'
import SkipBackward from 'vue-material-design-icons/SkipBackward.vue'


// Imports from pinia store
import { useSongStore } from '../stores/song'
import { storeToRefs } from 'pinia'


const useSong = useSongStore()

const { isPlaying, audio, currentTrack, currentArtist } = storeToRefs(useSong)

let isHover = ref(null)
let isTrackTimeCurrent = ref(null)
let isTrackTimeTotal = ref(null)
let seeker = ref(null)
let seekerContainer = ref(null)
let range = ref(0)

onMounted(() => {
    if (audio.value) {
        setTimeout(() => {
            timeupdate()
            loadmetadata()
        }, 300)
    }
    if (currentTrack.value) {
        seeker.value.addEventListener('change', () => {
            const time = audio.value.duration * (seeker.value.value/100)
            audio.value.currentTime = time
        })
        seeker.value.addEventListener('mousedown', () => {
            audio.value.pause()
            isPlaying.value = false
        })
        seeker.value.addEventListener('mouseup', () => {
            audio.value.play()
            isPlaying.value = true
        })
        seekerContainer.value.addEventListener('click', (e) => {
            const clickPosition = (e.pageX - seekerContainer.value.offsetLeft) / seekerContainer.value.offsetWidth
            const time = audio.value.duration * clickPosition
            audio.value.currentTime = time 
            seeker.value.value = (100 / audio.value.duration) * audio.value.currentTime
        })
    }
})

const timeupdate = () => {
    audio.value.addEventListener('timeupdate', () => {
        var minutes = Math.floor(audio.value.currentTime / 60)
        var seconds = Math.floor(audio.value.currentTime - minutes * 60)
        isTrackTimeCurrent.value = minutes + ':' + seconds.toString().padStart(2,'0')
        const value = (100 / audio.value.duration) * audio.value.currentTime
        range.value = value
        seeker.value.value = value
    })
}

const loadmetadata = () => {
    audio.value.addEventListener('loadedmetadata', () => {
        const duration = audio.value.duration
        const minutes = Math.floor(duration / 60)
        const seconds = Math.floor(duration % 60)
        isTrackTimeTotal.value = minutes + ':' + seconds.toString().padStart(2,'0')
    })
}

watch(() => audio.value, () => {
    timeupdate()
    loadmetadata()
})
watch(() => isTrackTimeCurrent.value, (time) => {
    if (time && time == isTrackTimeTotal.value) {
        useSong.nextSong(currentTrack.value)
    }
})
</script>
<template>
  <div 
    id="MusicPlayer"
    v-if="audio"
    class="fixed flex items-center justify-between bottom-0 w-full z-50 h-24 bg-[#181818] border-t border-t-[#272727]" 
  >
    <div class="flex items-center w-1/4">
        <div class="flext items-center ml4">
            <img class="rounded-sm shadow-xl" width="55" :src="currentArtist.albumCover" :alt="currentTrack.name">
            <div class="text-sm text-white hover:underline cursor-pointer">
                {{ currentTrack.name }}
            </div>
            <div class="text-xs text-gray-400 hover:underline hover:text-white cursor-pointer">
                {{ currentTrack.name }}
            </div>
        </div>
        <div class="flex items-center ml-8">
            <Heart class="text-green-500" :size='20'/>
            <PictureInPictureBottomRight class="text-white m-4" :size="18"/>
        </div>
    </div>
    <div class="max-w-[35%] mx-auto w-2/4 mb-3">
        <div class="flex-col items-center justify-center">
            <div class="flex items-center justify-center h-8">
                <button class="mx-2">
                    <SkipBackward class="text-white" :size="25" @click="useSong.prevSong(currentTrack)"/>
                </button>
                <button class="p-1 rounded-full mx-3 bg-white" @click=" useSong.playOrPauseThisSong(currentArtist, currentTrack)">
                    <Play v-if="!isPlaying" class="text-[#1818181]" :size="25"/>
                    <Pause v-else class="text-[#1818181]" :size="25"/>
                </button>
                <button class="mx-2">
                    <SkipFoward class="text-white" :size="25" @click="useSong.nextSong(currentTrack)"/>
                </button>
            </div>
        </div>
        <div class="flex items-center h-6">
            <div v-if="isTrackTimeCurrent" class="text-white text-xs pr-2 pt-3">
                {{ isTrackTimeCurrent }}
            </div>
            <div
                class="w-full relative mt-2 mb-3"
                ref="seekerContainer"
                @mouseenter="isHover = true"
                @mouseleave="isHover = false"
            >
                <input
                    type="range"
                    v-model="range"
                    ref="seeker"
                    class="absolute rounded-full my-2 w-full h-0 z-40 appearance-none bg-opacity-100 focus:outline-none accent-white"
                    :class="{'rangeDotHidden': !isHover}"
                >
                <div
                    class="pointer-events-none mt-1.5 absolute h-1 z-10 inset-y-0 left-0 w-0"
                    :style="`width:${range}%;`"
                    :class="[isHover ? 'bg-green-500' : 'bg-white']"
                />
                <div class="absolute h-1 -z-0 mt-1.5 inset-y-0 left-0 w-full bg-gray-500 rounded-full"></div>
            </div>
            <div v-if="isTrackTimeTotal" class="text-white text-xs pl-2 pt-3">
                {{ isTrackTimeTotal }}
            </div>
        </div>
    </div>
    <div class="flex items-center w-1/4 justify-end pr-10">
        <MusicPlayerVolume />
    </div>
  </div>
</template>
<style>
.rangeDotHidden[type='range']::-webkit-slider-thumb{
    -webkit-appearance: none;
    appearance: none;
    width: 0;
    height: 0;
}
</style>

