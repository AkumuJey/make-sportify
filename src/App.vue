<script setup>
import { ref } from 'vue';
import { RouterLink, RouterView } from 'vue-router'
import ChevronUp from'vue-material-design-icons/ChevronUp.vue'
import ChevronDown from'vue-material-design-icons/ChevronDown.vue'
import ChevronRight from'vue-material-design-icons/ChevronRight.vue'
import ChevronLeft from'vue-material-design-icons/ChevronLeft.vue'


let openMenu = ref(false)
</script>

<template>
<div>
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
            @click="openMenu = !openMen"
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
    </div>
</div>
</template>

<style >


</style>
