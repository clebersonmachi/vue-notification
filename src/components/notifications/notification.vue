<template>
    <div class="notificacao" :class="type">
        <button class="fechar" @click.prevent="close">
            X
        </button>
        <div class="nome">{{ name }}</div>
        <div class="descricao" if="description">{{ description }}</div>
        <div class="barra-progresso">
            <div class="progresso" :style="{ width: `${porcentage}%` }"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: "CmNotification",

    props: {
        id: {
            required: true
        },
        name: {
            type: String,
            required: true
        },
        description: {
            type: String
        },
        type: {
            type: String,
            default: "is-success"
        },
        time: {
            type: Number,
            default: 5000
        }
    },

    data() {
        return {
            now: this.time
        };
    },

    computed: {
        porcentage() {
            const total = parseInt(this.time);
            const now = parseInt(this.now);
            return (now / total) * 100;
        }
    },

    methods: {
        processTime() {
            let newNow = this.now - 100;
            if (newNow === 0) {
                this.$emit("finish", this.id);
            }

            this.now = newNow;
        },

        close() {
            this.$emit("finish", this.id);
        }
    },

    created() {
        setInterval(this.processTime, 100);
    }
};
</script>

<style>
.notificacao {
    position: relative;
    text-align: left;
    background-color: #fff;
    padding: 15px 20px;
    box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.2);
    margin-bottom: 30px;
}

.notificacao .fechar {
    position: absolute;
    top: 5px;
    right: 5px;
}

.notificacao .nome {
    font-weight: bold;
}

.notificacao .descricao {
    font-size: 12px;
}

.notificacao .barra-progresso {
    margin-top: 15px;
    background: #f2f2f2;
    height: 10px;
    border-radius: 30px;
}

.notificacao .barra-progresso .progresso {
    border-radius: 30px;
    height: 10px;
    background-color: #333;
    transition: width ease 0.1s;
}

.notificacao.is-success {
    border-left: 4px solid green;
}

.notificacao.is-error {
    border-left: 4px solid red;
}
</style>
