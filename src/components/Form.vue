<script lang="ts">
import { defineComponent } from "vue";
import TimerControl from "./TimerControl.vue";

export default defineComponent({
    name: "Form",
    components: { TimerControl },
    emits: ["onSaveTask"],
    methods: {
        finishTask(timePassed: number): void {
            this.$emit("onSaveTask", {
                durationInSeconds: timePassed,
                description: this.description,
            });
            this.description = "";
        },
    },
    data() {
        return {
            description: "",
        };
    },
});
</script>

<template>
    <div class="box form">
        <div class="columns">
            <div
                class="column is-8"
                role="form"
                aria-label="Formulário para criação de uma nova tarefa."
            >
                <input
                    type="text"
                    class="input"
                    placeholder="Qual tarefa você deseja iniciar?"
                    v-model="description"
                />
            </div>
            <div class="column">
                <TimerControl @on-timer-finish="finishTask" />
            </div>
        </div>
    </div>
</template>

<style>
.form {
    color: var(--text-primary);
    background-color: var(--bg-primary);
    box-shadow: none;
}

/* Overwriting Bulma Styles */
input {
    background-color: var(--bg-primary) !important;
    color: var(--text-primary) !important;
    border-color: var(--text-primary) !important;
}

input::placeholder {
    color: var(--text-primary) !important;
}
</style>
