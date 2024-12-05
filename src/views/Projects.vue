<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
    name: "Projects"
});
</script>

<template>
    <div class="projects">
        <h1 class="title">Projetos</h1>
        <router-view></router-view>
    </div>
</template>

<style scoped>
.projects {
    padding: 1.25rem;
}

h1 {
    color: var(--text-primary);
}
</style>