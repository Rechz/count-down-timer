<template>
    <div class="d-flex justify-content-center align-items-center flex-column main">
            <h1 class="head w-50 my-5">Countdown Timer</h1>
            <ParaCard :isPara="isPara"/>
            <div v-if="!timerOn" class="w-25 d-flex justify-content-center align-items-center flex-column">
                <input type="text" v-model.number="countdownTimer" class="form-control" @keypress.enter="setTimer">
                <button @click="setTimer" class="btn btn-outline-secondary mt-5"><span class="fa fa-play icon"></span></button>
            </div>
            <div v-else class="w-25 d-flex justify-content-center align-items-center flex-column">
                <div class="backstyle d-flex align-items-center justify-content-center" :class="{ 'glow': isGlowing }">
                    <h1 class="timer-view">{{ countTimer }}</h1>
                </div>
                <div class="mt-5 w-25 d-inline-flex justify-content-center" >
                    <button v-if="!restart" @click="pauseTimer" class="btn btn-outline-secondary me-3" ><span class="fa fa-pause icon"></span></button>
                    <button v-else @click="continueTimer" class="btn btn-outline-secondary me-3"><span class="fa fa-play icon"></span></button>
                    <button @click="resetTimer" class="btn btn-outline-secondary"><span class="fa fa-refresh icon"></span></button>
                </div>
            </div>
    </div>
</template>

<script>
import ParaCard from './ParaCard.vue';
export default {
    components: {
        ParaCard
    },
    data() {
        return {
            countdownTimer : null,
            countTimer : null,
            timer : null,
            timerOn : false,
            restart : false,
            isGlowing : false,
            isInput : false,
            isPara : false
        };
    },
    methods: {
        setTimer() {
            if(this.countdownTimer != null)
            {
                this.isInput = true;
                this.isPara = true;
            }
            if(this.isInput) {
                this.timerOn = true;
                this.countTimer = this.countdownTimer;
                this.countdownTimer = null;
                this.isGlowing =true
                this.timer = setInterval(()=> {
                    if (this.countTimer > 0) {
                        this.countTimer--;
                    }
                    else {
                        clearInterval(this.timer);
                        this.isGlowing = false; 
                        this.timerOn = false;
                        this.isPara = false;
                    }
                }, 1000)
            }
        },
        pauseTimer() {
            this.restart = !this.restart;
            this.isGlowing = false;
            clearInterval(this.timer)
        },
        resetTimer() {
            clearInterval(this.timer);
            this.countdownTimer = null;
            this.countTimer = null;
            this.timer = null;
            this.timerOn = false;
            this.restart = false;
            this.isInput = true;
            this.isPara = false;
        },
        continueTimer() {
            this.restart = !this.restart;
            this.isGlowing = true;
            this.timer = setInterval(()=> {
                if (this.countTimer > 0) {
                    this.countTimer--;
                }
                else {
                    clearInterval(this.timer);
                    this.isGlowing = false;
                    this.timerOn = false;    
                }
            }, 1000) 
        }
    },
  }

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron&family=Press+Start+2P&display=swap');
.main{
    height: 100vh;
}
.head {
    color: aliceblue;
    font-family: 'Press Start 2P', sans-serif;
    text-align: center;
}
.backstyle {
  width: 300px;
  height: 300px;
  border-radius: 50%;
  background-color: rgba(170, 168, 179, 0.481);
  box-shadow: 0 0 10px rgba(36, 35, 35, 0.3);
}
.glow {
    animation: glowAnimation 1s infinite;
}
@keyframes glowAnimation {
    0% {
        box-shadow: 0 0 20px rgba(255, 0, 0, 0.7); /* Red glow */
    }
    25% {
        box-shadow: 0 0 20px rgba(0, 0, 255, 0.7); /* Blue glow */
    }
    50% {
        box-shadow: 0 0 20px rgba(0, 255, 0, 0.7); /* Green glow */
    }
    75% {
        box-shadow: 0 0 20px rgba(255, 165, 0, 0.7); /* Orange glow */
    }
    100% {
        box-shadow: 0 0 20px rgba(255, 0, 0, 0.7); /* Red glow */
    }
}
.form-control {
    width: 300px !important;
    height: 300px !important;
    font-size: 5rem !important;
    box-shadow: 0 0 10px rgba(191, 186, 186, 0.3) !important; 
    background-color: rgba(170, 168, 179, 0.481) !important; 
    border-radius: 50% !important;
    text-align: center !important;
}   
.form-control:focus {
 background-color: rgba(207, 232, 232, 0.607) !important;
}
.btn {
    height: 70px;
    width: 100px;
}
.btn-outline-secondary {
    border: 2px solid white;
}
.btn-outline-secondary:focus {
background-color: rgba(255, 255, 255, 0.918);
}
.btn-outline-secondary:focus .icon{
    color: rgb(5, 6, 78);
}
.icon {
    font-size: 2rem;
    color: white;
}
.btn .icon{
    font-size: 3rem;
}
.timer-view {
    color: aliceblue;
    font-family: 'Orbitron', sans-serif;
    font-size: 6rem;
}
</style>