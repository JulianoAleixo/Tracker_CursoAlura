<script lang="ts">
import { defineComponent } from "vue";
import TimerControl from "./TimerControl.vue";
export default defineComponent({
    name: "Form",
    components: { TimerControl }
});
</script>

<template>
    <div class="box">
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
                />
            </div>
            <div class="column">
                <TimerControl />
            </div>
        </div>
    </div>
</template>

<style scoped></style>
