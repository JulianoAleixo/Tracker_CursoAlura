<script lang="ts">
import { defineComponent } from "vue";
import SideBar from "./components/SideBar.vue";
import FormComponent from "./components/FormComponent.vue";

export default defineComponent({
    name: "App",
    components: { SideBar, FormComponent }
});
</script>

<template>
    <main class="columns is-gapless is-multiline">
        <div class="column is-one-quarter">
            <SideBar />
        </div>
        <div class="column is-three-quarter">
            <FormComponent />
        </div>
    </main>
</template>

<style></style>
