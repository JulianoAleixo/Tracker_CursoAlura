<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "TimerButton",
    props: {
        isDisabled: { type: Boolean, default: false },
        text: { type: String, required: true },
        icon: { type: String, required: true },
    },
    emits: ["handleClick"],
});
</script>

<template>
    <button
        class="button"
        :class="{ 'disabled': isDisabled }"
        @click="$emit('handleClick')"
        :disabled="isDisabled"
    >
        <span class="icon">
            <i :class="`fas fa-${icon}`"></i>
        </span>
        <span>{{ text }}</span>
    </button>
</template>

<style scoped>
button {
    background: var(--bg-primary);
    color: var(--text-primary);
    border-color: var(--text-primary);
    border-width: 0.5px !important;
}

button:hover {
    background: var(--bg-hover);
}

button.disabled {
    background-color: var(--bg-disabled);
}
</style>
