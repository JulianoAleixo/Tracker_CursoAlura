<script lang="ts">
import { NotificationType } from "@/interfaces/INotification";
import { useStore } from "@/store";
import { EDIT_PROJECT, ADD_PROJECT, NOTIFICATE } from "@/store/mutations-type";
import { defineComponent } from "vue";

export default defineComponent({
    name: "Form",
    props: {
        id: { type: String },
    },
    mounted() {
        if (this.id) {
            const project = this.store.state.projects.find(
                (proj) => proj.id == this.id
            );
            this.projectName = project?.name || "";
        }
    },
    data() {
        return {
            projectName: "",
        };
    },
    methods: {
        save() {
            if (this.projectName.trim().length == 0) return;

            if (this.id) {
                this.store.commit(EDIT_PROJECT, {
                    id: this.id,
                    name: this.projectName,
                });
            } else {
                this.store.commit(ADD_PROJECT, this.projectName);
            }

            this.projectName = "";
            this.store.commit(NOTIFICATE, {
                title: "Novo projeto foi salvo",
                text: "Prontinho ;) seu projeto já está disponível",
                type: NotificationType.SUCCESS
            })
            this.$router.push("/projects");
        },
    },
    setup() {
        const store = useStore();
        return {
            store,
        };
    },
});
</script>

<template>
    <section class="projects">
        <form @submit.prevent="save">
            <div class="field">
                <label for="projectName" class="label"> Nome do Projeto </label>
                <input
                    type="text"
                    class="input"
                    v-model="projectName"
                    id="projectName"
                />
            </div>
            <div class="field">
                <button class="button my-button" type="submit">Salvar</button>
            </div>
        </form>
    </section>
</template>

<style scoped>
.projects {
    padding: 1.25rem;
}

h1 {
    color: var(--text-primary);
}

.my-button {
    background-color: var(--bg-button);
    color: var(--text-button);
}

.label {
    color: var(--text-primary);
}
</style>
