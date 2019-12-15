<template>
    <div id="app">
        <cm-notifications />

        <img alt="Vue logo" src="./assets/logo.png" />

        <div>
            <button @click="addNotification">Adicionar notificação</button>
        </div>

        <HelloWorld msg="Welcome to Your Vue.js App" />
    </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import CmNotifications from "./components/notifications/notifications";

export default {
    name: "app",
    components: {
        HelloWorld,
        CmNotifications
    },

    methods: {
        addNotification() {
            const notification = {
                name: "Primeira notificação",
                description: "Descrição",
                type: "is-success"
            };

            this.$root.$emit("add-notification", notification);
        }
    }
};
</script>

<style>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
