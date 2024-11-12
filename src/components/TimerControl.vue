<script lang="ts">
import { defineComponent } from "vue";
import Timer from "./Timer.vue";
import TimerButton from "./TimerButton.vue";

export default defineComponent({
    name: "TimerControl",
    emits: ["onTimerFinish"],
    components: { Timer, TimerButton },
    data() {
        return {
            timeInSeconds: 0,
            interval: 0,
            isTimerRunning: false,
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
            this.$emit("onTimerFinish", this.timeInSeconds);
            this.timeInSeconds = 0;
        },
    },
});
</script>

<template>
    <div class="is-flex is-align-items-center is-justify-content-space-around">
        <Timer :timeInSeconds="timeInSeconds" />
        <TimerButton
            :isDisabled="isTimerRunning"
            text="Play"
            icon="play"
            @click="handleStart"
        />
        <TimerButton
            :isDisabled="!isTimerRunning"
            text="Stop"
            icon="stop"
            @click="handleFinish"
        />
    </div>
</template>
