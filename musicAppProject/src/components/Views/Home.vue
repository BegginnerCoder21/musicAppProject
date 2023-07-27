<template>
    <div class="apps">
        <Header />
        <div class="composent" >
            <Music #nameMusic class="lismusic">
                <h3>{{ musicList[incrementmusic - 1].titleMusic }} -</h3>
                <h3>{{musicList[incrementmusic - 1].nameArtiste }}</h3>
            </Music>
        </div>
        <BoutonApp
            @next-music="nextMusic"
            @prev-music="prevMusic"
            :incrementmusic="incrementmusic"
        />
        <h2>The PlayList</h2>
        <DisplayMusicListVue 
            :musicList="musicList"
            :incrementmusic="incrementmusic"
        />
    </div>
</template>
<!-- v-for="list in musicList"  -->
<script setup lang="ts">

import Header from '@/components/MusicApp/Header.vue';
import BoutonApp from '@/components/MusicApp/BoutonApp.vue';
import Music from '@/components/MusicApp/Music.vue';
import DisplayMusicListVue from '../MusicApp/DisplayMusicList.vue';
import { reactive, ref ,onMounted} from 'vue';
import type Musics from '@/components/composables/index'

const nbmusic = ref<number>(0);
const incrementmusic = ref(1);
const musicList = reactive<Musics[]>([
    {
        id:Date.now(),
        titleMusic:'music1',
        nameArtiste:'Arafat',
        urlmusic:'Arafat'
    },
    {
        id:Date.now(),
        titleMusic:'music2',
        nameArtiste:'Gims',
        urlmusic:'Gims'
    },
    {
        id:Date.now(),
        titleMusic:'music3',
        nameArtiste:'Safarel',
        urlmusic:'Arafat'
    },
    {
        id:Date.now(),
        titleMusic:'music4',
        nameArtiste:'Nash',
        urlmusic:'Gims'
    },
]);


const nextMusic = (listerAudio:any) => {
    listerAudio[incrementmusic.value - 1].pause();
    if(incrementmusic.value === nbmusic.value){
        incrementmusic.value = 1;
        listerAudio[incrementmusic.value - 1].play();
    }else{
        incrementmusic.value++;
        listerAudio[incrementmusic.value - 1].play();
    }
}


const prevMusic = () => {
    if(incrementmusic.value === 1){
        incrementmusic.value = nbmusic.value;
    }else{
        incrementmusic.value--;
    }
}


onMounted(() => {
    nbmusic.value = document.querySelectorAll('#nbsmusic').length;
});
</script>

<style scoped>

.apps{
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
}

.apps h2{
    color: #313131;
    margin-top: 30px;
    margin-bottom: 20px;
    
}
.apps .composent{
    display: flex;
    gap:8px ;
    margin-top: 20px;
    justify-content: center;
    align-items: center;
 
}
.apps .composent .lismusic{
    display: flex;
    align-items: center;
}

.apps .composent  h3:last-of-type{
    font-weight: 400;
    font-style: italic;
    font-size: 22px;
}

</style>