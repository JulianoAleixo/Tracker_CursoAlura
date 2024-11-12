<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "Timer",
    props: {
        timeInSeconds: { type: Number, default: 0 }
    },
    computed: {
        timePassed(): string {
            return new Date(this.timeInSeconds * 1000)
                .toISOString()
                .substr(11, 8);
        },
    },
});
</script>

<template>
    <section>
        <strong class="timer-text">{{ timePassed }}</strong>
    </section>
</template>

<style>
.timer-text {
    color: var(--text-primary);
}
</style>
