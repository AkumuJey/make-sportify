<script setup>
// Vue imports
import { onMounted, ref, watch } from 'vue'

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
            audio.value.Pause()
            isPlaying.value = false
        })
        seeker.value.addEventListener('mouseup', () => {
            audio.value.Play()
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
    audio.value.addEventListener('loadmetadata', () => {
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
    if (time && time === isTrackTimeTotal.value) {
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
            <div class="text-xs text-gray-400 hover:underline cursor-pointer">
                {{ currentTrack.name }}
            </div>
        </div>
    </div>
  </div>
</template>


