<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
    name: "FormComponent",
    data() {
        return {
            timeInSeconds: 0,
            interval: 0
        };
    },
    computed: {
        timePassed(): string {
            return new Date(this.timeInSeconds * 1000)
                .toISOString()
                .substr(11, 8);
        },
    },
    methods: {
        handleStart() {
            this.interval = setInterval(() => {
                this.timeInSeconds += 1;
            }, 1000);
        },
        handleFinish() {
            clearInterval(this.interval);
        },
    },
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
                <div
                    class="is-flex is-align-items-center is-justify-content-space-between"
                >
                    <section>
                        <strong>{{ timePassed }}</strong>
                    </section>

                    <button class="button" @click="handleStart()">
                        <span class="icon">
                            <i class="fas fa-play"></i>
                        </span>
                        <span>Play</span>
                    </button>
                    <butotn class="button" @click="handleFinish()">
                        <span class="icon">
                            <i class="fas fa-stop"></i>
                        </span>
                        <span>Stop</span>
                    </butotn>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
</style>
