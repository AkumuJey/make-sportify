<script setup>
import SongRow from '../components/SongRow.vue'
import Play from 'vue-material-design-icons/Play.vue'
import Pause from 'vue-material-design-icons/Pause.vue'
import DotsHorizontal from 'vue-material-design-icons/DotsHorizontal.vue'
import Heart from 'vue-material-design-icons/Heart.vue'
import ClockTimeThreeOutline from 'vue-material-design-icons/ClockTimeThreeOutline.vue'
import artist from '../artist.json'

import { useSongStore } from '../stores/song'
import { storeToRefs } from 'pinia'


const useSong = useSongStore()

const { isPlaying, currentTrack, currentArtist } = storeToRefs(useSong)

const playfunc = () => {
    if (currentTrack.value) {
        useSong.playOrPauseThisSong(currentArtist.value, currentTrack.value)
        return
    }
    useSong.playFromFirst()
}
</script>
<template>
    <div>
        <div class="p-8">
          <button
            type="button"
            class="text-white text-2xl font-semibold hover:underline cursor-pointer"
          >
            {{ artist.name }}
          </button>
          <div class="py-1.5"></div>
          <div class="flex items-center w-full relative h-full">
            <img width="140" :src="artist.albumCover" :alt="artist.name">
            <div class="w-full ml-5">
                <div
                    class="text-white text-4xl absolute w-full hover:underline cursor-pointer top-0 font-semibold"
                >
                    {{ artist.name }}
                </div>
                <div class="text-gray-300 text-sm flex">
                    <div class="flex">Album</div>
                    <div class="ml-2 flex">
                        <div class="circle mt-2 mr-2"></div>
                        <span class="-ml-0.5">{{ artist.releaseYear }}</span>
                    </div>
                    <div class="ml-2 flex">
                        <div class="circle mt-2 mr-2"></div>
                        <span class="-ml-0.5">{{ artist.tracks.length }} songs</span>
                    </div>
                    <div class="absolute flex gap-4 items-center justify-start bottom-0 mb-1.5">
                        <button type="button" class="p-1 rounded-full bg-white" @click="playfunc()">
                            <Play v-if="!isPlaying" fillColor="#1818181" :size="25"/>
                            <Pause v-else fillColor="#1818181" :size="25"/>
                        </button>
                        <button type="button">
                            <Heart v-if="true" class="text-green-500" :size="30"/>                            <Play v-else fillColor="#1818181" :size="25"/>
                        </button>
                        <button type="button">
                            <DotsHorizontal v-if="true" fillColor="#FFFFFF" :size="25"/>                            <Play v-else fillColor="#1818181" :size="25"/>
                        </button>
                    </div>
                </div>
            </div>
          </div>
        </div>
        <div class="mt-6"></div>
        <div class="flex items-center justify-between px-5 pt-2">
            <div class="flex items-center justify-between text-gray-400">
                <div class="mr-7">#</div>
                <div class="text-sm">Title</div>
            </div>
            <div>
                <ClockTimeThreeOutline class="text-white" :size="18"/>
            </div>
        </div>
        <div class="border-b border-b-[#2A2A2A] mt-2"></div>
        <div class="mb-4"></div>
        <ul class="w-full" v-for="track,index in artist.tracks" :key="track">
            <SongRow :artist="artist" :track="track" :index="++index"/>
        </ul>
    </div>
</template>
