<script lang="ts">
import { defineComponent } from "vue";
import Timer from "./Timer.vue";
export default defineComponent({
    name: "TimerControl",
    components: { Timer },
    data() {
        return {
            timeInSeconds: 0,
            interval: 0,
            isTimerRunning: false
        };
    },
    methods: {
        handleStart() {
            this.isTimerRunning = true;
            this.interval = setInterval(() => {
                this.timeInSeconds += 1;
            }, 1000);
        },
        handleFinish() {
            this.isTimerRunning = false;
            clearInterval(this.interval);
        },
    },
});
</script>

<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <Timer :timeInSeconds="timeInSeconds" />
        <button class="button" @click="handleStart()" :disabled="isTimerRunning">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>Play</span>
        </button>
        <button class="button" @click="handleFinish()" :disabled="!isTimerRunning">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>Stop</span>
        </button>
    </div>
</template>
