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
        <div>
            <button class="button my-button" @click="changeTheme">
                {{ buttonText }}
            </button>
        </div>
        <nav class="pannel">
            <ul>
                <li>
                    <router-link to="/" class="link">
                        <i class="fas fa-tasks"></i>
                        Tarefas
                    </router-link>
                </li>
                <li>
                    <router-link to="/projects" class="link">
                        <i class="fas fa-project-diagram"></i>
                        Projetos
                    </router-link>
                </li>
            </ul>
        </nav>
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

.my-button {
    background-color: var(--bg-button);
    color: var(--text-button);
}

.pannel li {
    margin: 8px 0;
}

.link {
    color: #fff;
}

.link:hover {
    color: #FAF0CA;
}

.link.router-link-active {
    color: #FAF0CA;
}

@media only screen and (max-width: 768px) {
    header {
        padding: 2.5rem;
        height: auto;
    }
}
</style>
