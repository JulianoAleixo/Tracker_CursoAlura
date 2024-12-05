<script lang="ts">
import { defineComponent } from "vue";
import Form from "../components/Form.vue";
import Task from "../components/Task.vue";
import ITask from "../interfaces/ITasks";
import Box from "../components/Box.vue";

export default defineComponent({
    name: "App",
    components: { Form, Task, Box },
    data() {
        return {
            tasks: [] as ITask[],
        };
    },
    methods: {
        saveTask(task: ITask): void {
            this.tasks.push(task);
        },
    },
    computed: {
        isTasksEmpty(): boolean {
            return this.tasks.length === 0;
        },
    },
});
</script>

<template>
    <Form @onSaveTask="saveTask" />
    <div class="list">
        <Task v-for="(task, index) in tasks" :key="index" :task="task" />
        <Box v-if="isTasksEmpty"> Você não fez nenhuma tarefa ainda. </Box>
    </div>
</template>

<style>
.list {
    padding: 1.25rem;
}
</style>
