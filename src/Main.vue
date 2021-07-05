<template>

<div class="container">
    <div class="container__timer">
        <span class="container__minute">{{minutes}}</span>
        <span>:</span>
        <span class="container__seconds"> {{seconds}} </span>
    </div>
    <div class="container__controls">
        <button class="container__play" v-if="startButton" @click="startTimer">Play</button>
        <button class="container__stop" v-if="stopButton" @click="stopTimer">Stop</button>
        <button class="container__reset" v-if="resetButton" @click="resetTimer" >Reset</button>
    </div>
</div>    
</template>

<script>
import {ref} from 'vue'
export default {
    setup() {
        
            let minutes = ref(1);
            let seconds = ref('00');
            let timer = null;
            let resetButton= ref(false);
            let startButton = ref(true);
            let stopButton = ref(false);
           

        function startTimer() {
          seconds.value=59;
          minutes.value=0;
          timer = setInterval(() => {countdown()},1000);
          this.resetButton = true;
          this.startButton = false;
          this.stopButton = true;
        
        }
        function stopTimer() {
          clearInterval(timer);
          timer = null;
          this.resetButton = true;
          this.startButton = true;
          this.stopButton = false;

        
        }
        function resetTimer() {
          seconds.value = "00";
          minutes.value = 1;
          clearInterval(timer);
          timer = null;
          this.resetButton = false;
          this.startButton = true;
          this.stopButton = false;
        }
        function countdown() {
        
          seconds.value--;
          if(seconds.value == -1){
            alert("Zaman resetleniyor");
            resetTimer();
          }
        }
        return{
            minutes,
            seconds,
            startTimer,
            stopTimer,
            resetTimer,
            resetButton,
            startButton,
            stopButton            
        }
        
    },
   
};
</script>


<style lang="scss">

body{
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: burlywood;

.container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 40vw;
    &__timer{
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items:center;
        font-size: 72px;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }
    &__play {
        height: 50px;
        width: 75px;
        border: none;
        margin: 10px;
        border-radius: 35px;
        font-size: 18px;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        color: white;
        background-color: rgb(22, 112, 0);

    }
    &__reset {
        height: 50px;
        width: 75px;
        border: none;
        margin: 10px;
        border-radius: 35px;
        font-size: 18px;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        color: white;
        background-color: rgb(0, 0, 0);

    }
    &__stop{
        height: 50px;
        width: 75px;
        border: none;
        margin: 10px;
        border-radius: 35px;
        font-size: 18px;
        font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        color: white;
        background-color: rgb(255, 0, 0);

    }
   
}
}
</style>