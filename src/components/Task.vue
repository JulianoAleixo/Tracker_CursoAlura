<script lang="ts">
import { defineComponent, PropType } from "vue";
import Timer from "./Timer.vue";
import ITask from "@/interfaces/ITasks";
import Box from "./Box.vue";

export default defineComponent({
    name: "Task",
    components: { Timer, Box },
    props: {
        task: { type: Object as PropType<ITask>, required: true },
    },
});
</script>

<template>
    <Box class="box has-text-weight-bold">
        <div class="columns">
            <div class="column is-7">{{ task.description || 'Tarefa sem descrição' }}</div>
            <div class="column">
                <Timer :timeInSeconds="task.durationInSeconds" />
            </div>
        </div>
    </Box>
</template>

<style scoped>
</style>
