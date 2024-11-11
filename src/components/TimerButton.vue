<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "TimerButton",
    props: {
        isDisabled: { type: Boolean, default: false },
        text: { type: String, required: true },
        icon: { type: String, required: true },
    },
    emits: ['handleClick']
});
</script>

<template>
    <button class="button" @click="$emit('handleClick')" :disabled="isDisabled">
        <span class="icon">
            <i :class="`fas fa-${icon}`"></i>
        </span>
        <span>{{ text }}</span>
    </button>
</template>

<style scoped></style>