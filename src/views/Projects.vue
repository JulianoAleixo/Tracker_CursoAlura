<script lang="ts">
import IProject from '@/interfaces/IProject';
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'Projects',
    data() {
        return {
            projectName: "",
            projects: [] as IProject[]
        };
    },
    methods: {
        save() {
            const project: IProject = {
                name: this.projectName,
                id: new Date().toISOString()
            }
            this.projects.push(project);
            this.projectName = '';
        }
    }
});
</script>

<template>
    <section class="projects">
        <h1>Projetos</h1>
        <form @submit.prevent="save">
            <div class="field">
                <label for="projectName" class="label">
                    Nome do Projeto
                </label>
                <input type="text" class="input" v-model="projectName" id="projectName">
            </div>
            <div class="field">
                <button class="button my-button" type="submit">
                    Salvar
                </button>
            </div>
        </form>
        <table class="table is-fullwidth mt-5">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Nome</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="project in projects" :key="project.id">
                    <td>{{ project.id }}</td>
                    <td>{{ project.name }}</td>
                </tr>
            </tbody>
        </table>
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