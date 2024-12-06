<script lang="ts">
import { computed, defineComponent } from "vue";
import TimerControl from "./TimerControl.vue";
import { NOTIFICATE } from "@/store/mutations-type";
import { NotificationType } from "@/interfaces/INotification";
import { useStore } from "@/store";

export default defineComponent({
    name: "Form",
    components: { TimerControl },
    emits: ["onSaveTask"],
    methods: {
        finishTask(timePassed: number): void {
            if (!this.idProject) {
                this.store.commit(NOTIFICATE, {
                    title: "[Erro] Sem Projeto",
                    text: "Você está tentando criar uma tarefa sem um projeto associado. Tente novamente.",
                    type: NotificationType.FAIL,
                });
                this.description = "";
                return;
            }

            this.$emit("onSaveTask", {
                durationInSeconds: timePassed,
                description: this.description,
                project: this.projects.find(
                    (proj) => proj.id == this.idProject
                ),
            });
            this.description = "";
            this.idProject = "";
        },
    },
    data() {
        return {
            description: "",
            idProject: "",
        };
    },
    setup() {
        const store = useStore();
        return {
            projects: computed(() => store.state.projects),
            store
        };
    },
});
</script>

<template>
    <div class="box form">
        <div class="columns">
            <div
                class="column is-5"
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

            <div class="column is-3">
                <div class="select">
                    <select v-model="idProject" class="my-select">
                        <option value="">Selecione o Projeto</option>
                        <option
                            :value="project.id"
                            v-for="project in projects"
                            :key="project.id"
                        >
                            {{ project.name }}
                        </option>
                    </select>
                </div>
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

.my-select {
    background: var(--bg-primary) !important;
    color: var(--text-button) !important;
    border-color: var(--text-primary) !important;
}
</style>
