<template>
    <div class="lista-notificacoes">
        <transition-group name="list" tag="div">
            <cm-notification
                v-for="notification in notifications"
                :id="notification.id"
                :name="notification.name"
                :description="notification.description"
                :type="notification.type"
                :key="notification.id"
                @finish="onFinishNotification"
            />
        </transition-group>
    </div>
</template>

<script>
import CmNotification from "./notification";

export default {
    components: {
        CmNotification
    },

    data() {
        return {
            notifications: []
        };
    },

    methods: {
        onFinishNotification(id) {
            const notifications = this.notifications;
            for (let index = 0; index < notifications.length; index++) {
                const notification = notifications[index];
                if (notification.id === id) {
                    notifications.splice(index, 1);
                    break;
                }
            }
        },

        addNotification(notification) {
            if (!notification.id) {
                notification.id = Date.now();
            }

            this.notifications.push(notification);
        }
    },

    created() {
        this.$root.$on("add-notification", this.addNotification);
    },

    beforeDestroy() {
        this.$root.$off("add-notification", this.addNotification);
    }
};
</script>

<style>
.lista-notificacoes {
    position: fixed;
    right: 0;
    top: 0;
    padding: 30px;
    width: 320px;
    max-height: 100%;
    overflow: hidden;
    z-index: 90000;
}

.list-item {
    display: inline-block;
    margin-right: 10px;
}
.list-enter-active,
.list-leave-active {
    transition: all ease-in-out 0.4s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
    opacity: 0;
    transform: translateX(100%);
}
</style>
