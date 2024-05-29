<template>
  <div id="app">
    <header class="text-center p-3" >
      <h1>Sala de Chat</h1>
    </header>

    <main class="container">
      <div class="row" >
        <section class="col-12 col-lg-3" v-if="usuarios.length > 0">
          <CardUsers 
          :usuario="usuarios[0]"
          @enviarMensaje="mostrarMensaje"
          />
        </section>

        <section class="col-12 col-lg-6" >
          <ChatUser :mensajes="mensajes" :usuarios="usuarios" />
        </section>

        <section class="col-12 col-lg-3" v-if="usuarios.length > 0">
          <CardUsers 
          :usuario="usuarios[1]"
          @enviarMensaje="mostrarMensaje"
          />
        </section>
      </div>


    </main>

  </div>
</template>

<script>
import axios from 'axios';
import CardUsers from './components/CardUsers.vue';
import ChatUser from './components/ChatUser.vue';

export default {
  name: 'App',
  components: {
    CardUsers,
    ChatUser
  },
  data() {
    return {
      usuarios: [],
      mensajes: []
    }
  },
  methods: {
    mostrarMensaje(mensaje) {
      let nuevoMensaje = {
        id: mensaje.id,
        color: mensaje.color,
        nombreUsuario: mensaje.nombreUsuario,
        msg: mensaje.msg,
      }
      this.mensajes.push(nuevoMensaje);
      
    }
  },
  async mounted() {
    try {
      let response = await axios.get("https://randomuser.me/api/?results=2");
      let { data } = response;
      this.usuarios = data.results;
      console.log(this.usuarios)
    } catch (error) {
      console.log(error);
      if (error.code == "ERR_NETWORK") {
        return alert("En estos momento el servidor está caído, puede intentar más tarde.")
      }
      if (error.response.status == 404) {
        alert("El recurso que está buscando no existe.");
      } else {
        alert("El servidor en estos momentos no puede procesar su solicitud.")
      }
    }

  }
}
</script>

<style></style>
