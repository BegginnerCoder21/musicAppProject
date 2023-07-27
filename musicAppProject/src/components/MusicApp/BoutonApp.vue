<template>
    <div class="inputDiv">
        <input type="submit" value="Prev" @click="$emit('prev-music')">
        <input class="inputPlay" type="submit" :value="[PlayOrPause ? 'Pause' : 'Play']" @click="playAudio">
        <input type="submit" value="Next" @click="$emit('next-music',listerAudio)">
    </div>
</template>

<script setup lang="ts">
import { computed, onMounted, ref } from 'vue';

const PlayOrPause = ref(false);
const listerAudio = ref();
const props = defineProps<{
    incrementmusic:number
}>();
const playAudio = () => {
    if(listerAudio.value[props.incrementmusic - 1].paused){
        PlayOrPause.value = true
        listerAudio.value[props.incrementmusic - 1].play();
    }else{
        PlayOrPause.value = false
        listerAudio.value[props.incrementmusic - 1].pause();
    }
}


onMounted(() => {
     listerAudio.value = document.querySelectorAll('#lectureAudio');
})

</script>

<style scoped>

.inputDiv{
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 30px;
    gap: 20px;
    
}

.inputDiv input{
    padding: 7px 23px;
    border-radius: 5px;
    color: #fff;
    cursor: pointer;
    outline: none;
    border: none;
}

.inputDiv .inputPlay{
    background-color: rgb(230, 51, 15); 
    padding: 10px 30px;
   
}
.inputDiv .inputPlay:hover{
    background-color: rgb(246, 90, 59);
}

    .inputDiv input:last-of-type,
.inputDiv input:first-of-type{
    background-color: rgb(227, 107, 27);
}

.inputDiv input:last-of-type:hover,
.inputDiv input:first-of-type:hover{
    background-color: rgb(244, 134, 62);
}

</style>