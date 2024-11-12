<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
    name: "SideBar",
    emits: ['onChangeTheme'],
    data() {
        return {
            darkModeActive: false,
        }
    },
    methods: {
        changeTheme() {
            this.darkModeActive = !this.darkModeActive;
            this.$emit('onChangeTheme', this.darkModeActive);
        }
    }, 
    computed: {
        buttonText() {
            if (this.darkModeActive) {
                return 'Desativar modo escuro';
            } 
            return 'Ativar modo escuro'
        }
    }
});
</script>

<template>
    <header>
        <h1>
            <img src="../assets/logo.jpg" alt="" class="sidebar-logo" />
        </h1>
        <button class="button" @click="changeTheme">
            {{ buttonText }}
        </button>
    </header>
</template>

<style scoped>
header {
    background: #0d3b66;
    width: 100%;
    padding: 1rem;
    height: 100vh;
    text-align: center;
}

.sidebar-logo {
    margin: auto;
    height: auto;
    border-radius: 10px;
    object-fit: contain;
    display: block;
}

button {
    margin: 1.5rem;
}

@media only screen and (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}
</style>
