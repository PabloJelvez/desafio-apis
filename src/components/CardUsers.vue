<template>
    <div class="card cardContainer p-2">
        <div class="text-center">
            <img :src="usuario.picture.large" alt="" />
        </div>
        <div class="card-body">
            <div>
                <input class="inputColor" type="color" v-model="mensaje.color" />
            </div>
            <div>
                <p>{{ nombreUsuario }}</p>
            </div>
            <div>
                <textarea  class="textArea" name="mensaje" id="mensaje" v-model="mensaje.msg" @keyup.enter="enviarMensaje" ></textarea>

                <div>
                    <button @click.prevent="enviarMensaje" class="btn btn-info">
                        Enviar mensaje
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "CardUsers",
    props: {
        usuario: Object,
    },
    data() {
        return {
            mensaje: {
                msg: "",
                color: "#07c37b",
                id: "",
            },
        };
    },
    computed: {
        nombreUsuario() {
            return `${this.usuario.name.first} ${this.usuario.name.last}`;
        },
    },
    methods: {
        enviarMensaje() {
            this.mensaje.id = this.usuario.id.value;
            this.mensaje.nombreUsuario = this.nombreUsuario;
            this.$emit("enviarMensaje", this.mensaje);
            this.mensaje.msg = "";
        },
    },
};
</script>

<style scoped>
.card img {
    width: 90%;
}

.card-body {
    display: flex;
    flex-direction: column;
}
.inputColor{
    width:99%;
}
.textArea{
    width: 99%;
}
.btn{
    width: 99%;
}
</style>
