<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
    name: "SideBar",
});
</script>

<template>
    <header>
        <h1>
            <img src="../assets/logo.jpg" alt="" class="sidebar-logo" />
        </h1>
    </header>
</template>

<style scoped>
header {
    background: #0d3b66;
    width: 100%;
    padding: 1rem;
    height: 100vh;
}

.sidebar-logo {
    margin: auto;
    height: auto;
    border-radius: 10px;
    object-fit: contain;
    display: block;
}

@media only screen and (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}
</style>
