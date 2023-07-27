<template>
    <div>
        <ul>
            <li id="nbsmusic" v-for="(mslist,index) in props.musicList" :key="index" :class="{colormusic : index + 1 === incrementmusic}">
                <span>{{ mslist.titleMusic }} - {{ mslist.nameArtiste }} </span>
                <audio id="lectureAudio">
                    <source :src="getAudioPath(mslist.urlmusic)" type="audio/mpeg">
                </audio>
            </li>
        </ul>
    </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue';
import type Musics from '../composables';

const props = defineProps<{
    musicList:Musics[],
    incrementmusic:number
}>();

const getAudioPath = (mslist:string) => {
    return new URL(`../../assets/${mslist}.mp3`,import.meta.url).pathname;
}

</script>

<style scoped>

ul{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    
}

ul li{
    display: flex;
    padding: 10px;
    margin-bottom: 20px ;
    width: 35%;
    column-gap: 20px;
    justify-content:center;
    align-items: center;
}

ul .colormusic{
    border: none;
    background:linear-gradient(45deg,rgb(230, 51, 15),rgb(246, 90, 59)) ;
}

ul li span:hover{
    color: rgb(246, 90, 59);
}

</style>