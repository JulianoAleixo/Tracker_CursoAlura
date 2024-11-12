<script lang="ts">
import { defineComponent } from "vue";
import SideBar from "./components/SideBar.vue";
import Form from "./components/Form.vue";
import Task from "./components/Task.vue";
import ITask from "./interfaces/ITasks";
import Box from "./components/Box.vue";

export default defineComponent({
    name: "App",
    components: { SideBar, Form, Task, Box },
    data() {
        return {
            tasks: [] as ITask[],
            darkModeActive: false
        }
    },
    methods: {
        saveTask(task: ITask): void {
            this.tasks.push(task);
        },
        changeTheme(darkModeActive: boolean): void {
            this.darkModeActive = darkModeActive;
        }
    },
    computed: {
        isTasksEmpty(): boolean {
            return this.tasks.length === 0;
        }
    }
});
</script>

<template>
    <main class="columns is-gapless is-multiline" :class="{ 'dark-mode': darkModeActive }">
        <div class="column is-one-quarter">
            <SideBar @onChangeTheme="changeTheme"/>
        </div>
        <div class="column is-three-quarter content">
            <Form @onSaveTask="saveTask" />
            <div class="list">
                <Task v-for="(task, index) in tasks" :key="index" :task="task" />
                <Box v-if="isTasksEmpty">
                    Você não fez nenhuma tarefa ainda.
                </Box>
            </div>
        </div>
    </main>
</template>

<style>
main {
    --bg-primary: #FFF;
    --text-primary: #000;
    --bg-hover: #dcdcdc;
    --bg-disabled: #b8b8b8;
}

main.dark-mode {
    --bg-primary: #2B2D42;
    --text-primary: #DDD;
    --bg-hover: #222435;
    --bg-disabled: #191a27;
}

.content {
    background-color: var(--bg-primary);
}

.list {
    padding: 1.25rem;
}
</style>
