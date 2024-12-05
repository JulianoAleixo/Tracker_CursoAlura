<script lang="ts">
import { useStore } from '@/store';
import { DELETE_PROJECT } from '@/store/mutations-type';
import { computed, defineComponent } from 'vue';

export default defineComponent({
    name: 'List',
    methods: {
        handleDelete(id: string) : void {
            this.store.commit(DELETE_PROJECT, id);
        }
    },
    setup() {
        const store = useStore()
        return {
            projects: computed(() => store.state.projects),
            store
        }
    }
});
</script>

<template>
    <section class="projects">
        <router-link to="/projects/new" class="button my-button">
            <span class="icon is-small">
                <i class="fas fa-plus"></i>
            </span>
            <span>Novo Projeto</span>
        </router-link>

        <table class="table is-fullwidth mt-5">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Nome</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="project in projects" :key="project.id">
                    <td>{{ project.id }}</td>
                    <td>{{ project.name }}</td>
                    <td>
                        <router-link :to="`/projects/${project.id}`" class="button my-button">
                            <span class="icon is-small">
                                <i class="fas fa-pencil-alt"></i>
                            </span>
                        </router-link>

                        <button class="button ml-2 is-danger" @click="handleDelete(project.id)">
                            <span class="icon is-small">
                                <i class="fas fa-trash"></i>
                            </span>
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
    </section>
</template>

<style scoped>
.my-button {
    background-color: var(--bg-button);
    color: var(--text-button);
}

.label {
    color: var(--text-primary);
}
</style>