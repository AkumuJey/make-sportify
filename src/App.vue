<script setup>
import { ref } from 'vue';
import { RouterLink, RouterView } from 'vue-router'
import ChevronUp from'vue-material-design-icons/ChevronUp.vue'
import ChevronDown from'vue-material-design-icons/ChevronDown.vue'
import ChevronRight from'vue-material-design-icons/ChevronRight.vue'
import ChevronLeft from'vue-material-design-icons/ChevronLeft.vue'
import MenuItem from './components/MenuItem.vue'

let openMenu = ref(false)
</script>

<template>
<main>
    <div class="
        w-[calc(100%-240px)]
        h-[60px]
        fixed
        right-0
        z-20
        bg-[#101010]
        bg-opacity-80 flex
        items-center
        justify-between
        "
    >
        <div class="flex items-center ml-6 gap-4">
            <button type="button" class="rounded-full bg-black p-[1px] cursor-pointer">
                <ChevronLeft fillColor="#FFFFFF" :size="30"/>
            </button>
            <button type="button" class="rounded-full bg-black p-[1px] cursor-pointer">
                <ChevronRight fillColor="#FFFFFF" :size="30"/>
            </button>
        </div>
        <button
            type="button"
            @click="openMenu = !openMenu"
            :class="{ 'bg-[#282828]' : openMenu}" 
            class="bg-black hover:bg-[#282828] rounded-full p-0.5 mr-8 mt-0.5 cursor-pointer"
        >
            <div class="flex items-center gap-1 p-1">
                <img
                    class="rounded-full"
                    width="27"
                    src="https://yt3.ggpht.com/yti/AHXOFjWCLnuPczLwfMPR6Q5AeLSgle5MXA-X60kI9QDLRg=s88-c-k-c0x00ffffff-no-rj-mo"
                    alt="My Image"
                >
                <div class="text-white text-sm ml-1.5 font-semibold">Akumu Jey</div>
                <ChevronDown v-if="!openMenu" @click="openMenu = true" fillColor="#FFFFFF" :size="25"/>
                <ChevronUp v-else @click="openMenu = false" fillColor="#FFFFFF" :size="25"/>
            </div>
        </button>
        <span 
            v-if="openMenu"
            class="fixed w-48 bg-[#282828] shadow-xl z-50 rounded-xl top-[52px] right-9 p-1 cursor-pointer"
        >
            <ul class="text-gray-200 font-semibold text-sm">
                <li class="px-3 py-2 hover:bg-[#3E3D3D] border-b border-gray-600">Profile</li>
                <li class="px-3 py-2 hover:bg-[#3E3D3D] border-b border-gray-600">Logout</li>
            </ul>
        </span>
    </div>
    <div 
      id="sideNav"
      class="h-[100%] p-6 w-60 fixed z-50 bg-black"
    >
      <router-link to="/">
        <img width="125" src="/images/icons/spotify-logo.png" alt="">
      </router-link>
      <div class="my-8"></div>
      <ul>
        <router-link to="/">
            <MenuItem class="ml-[1px]" :icon-size="23" name="Home" iconString="home" pageUrl="/"/>
        </router-link>
        <router-link to="/search">
            <MenuItem class="ml-[1px]" :icon-size="24" name="Search" iconString="search" pageUrl="/search"/>
        </router-link>
        <router-link to="/library">
            <MenuItem class="ml-[2px]" :icon-size="23" name="Library" iconString="library" pageUrl="/library"/>
        </router-link>
        <div class="py-3.5"></div>
        <MenuItem class="ml-[1px]" :icon-size="24" name="Create Playlist" iconString="playlist" pageUrl="/playlist"/>
        <MenuItem class="-ml-[1px]" :icon-size="27" name="Like Songs" iconString="liked" pageUrl="/liked"/>
      </ul>
      <div class="border-b border-b-gray-700"></div>
      <ul>
        <ul class="font-semibold text-sm mt-3 text-gray-300 hover:text-white">My Playlist #1</ul>
        <ul class="font-semibold text-sm mt-3 text-gray-300 hover:text-white">My Playlist #2</ul>
        <ul class="font-semibold text-sm mt-3 text-gray-300 hover:text-white">My Playlist #3</ul>
        <ul class="font-semibold text-sm mt-3 text-gray-300 hover:text-white">My Playlist #4</ul>
        <ul class="font-semibold text-sm mt-3 text-gray-300 hover:text-white">My Playlist #5</ul>
        <ul class="font-semibold text-sm mt-3 text-gray-300 hover:text-white">My Playlist #6</ul>
      </ul>
    </div>
    <div
    class="fixed right-0 top-0 w-[calc(100%-240px)] overflow-auto h-full bg-gradient-to-b from-[#1c1c1c] to-black"
    >
        <div class="mt-[70px]"></div>
        <RouterView />
        <div class="mb-[100px]"></div>
    </div>
</main>
</template>

<style >


</style>
