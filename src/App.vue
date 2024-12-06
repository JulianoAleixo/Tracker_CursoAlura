<script lang="ts">
import { defineComponent } from "vue";
import SideBar from "./components/SideBar.vue";
import Notifications from "./components/Notifications.vue";

export default defineComponent({
    name: "App",
    components: { SideBar, Notifications },
    data() {
        return {
            darkModeActive: false
        }
    },
    methods: {
        changeTheme(darkModeActive: boolean): void {
            this.darkModeActive = darkModeActive;
        }
    }
});
</script>

<template>
    <main class="columns is-gapless is-multiline" :class="{ 'dark-mode': darkModeActive }">
        <div class="column is-one-quarter">
            <SideBar @onChangeTheme="changeTheme"/>
        </div>
        <div class="column is-three-quarters content">
            <Notifications />
            <router-view></router-view>
        </div>
    </main>
</template>

<style>
main {
    --bg-primary: #FFF;
    --text-primary: #000;
    --bg-hover: #dcdcdc;
    --bg-disabled: #b8b8b8;
    --bg-button: #dcdcdc;
    --text-button: #000;
    --bg-table: #dcdcdc;
}

main.dark-mode {
    --bg-primary: #2B2D42;
    --text-primary: #DDD;
    --bg-hover: #222435;
    --bg-disabled: #191a27;
    --bg-button: #3e3e3e;
    --text-button: #fff;
    --bg-table: #3e3e3e;
}

.content {
    background-color: var(--bg-primary);
}
</style>
