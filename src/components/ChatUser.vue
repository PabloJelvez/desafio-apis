<template>
  <div class="chatUser p-3">
    <h3 class="text-center">Mensajes</h3>
    <div ref="chatContainer" class="chatContainer">
      <div v-for="(mensaje, index) in mensajes" :key="index" >
        <p class="p-2 m-2 nombreUsuario" :style="{
            textAlign: mensaje.id === usuarios[0].id.value ? 'left' : 'right',
          }" >
          <small>{{ mensaje.nombreUsuario }}</small>
        </p>
        <p :style="{
            textAlign: mensaje.id === usuarios[0].id.value ? 'left' : 'right',
          }">
          <span class="spanMsg p-2 m-2" :style="{ backgroundColor: mensaje.color }">{{ mensaje.msg }}</span>
        </p>
      </div>
    </div>
    <br>
  </div>
</template>

<script>
export default {
  name: 'ChatUser',
  props: {
    usuarios: Array,
    mensajes: Array
  },
  watch: {
    mensajes() {
      this.$nextTick(() => {
        this.$refs.chatContainer.scrollTop = this.$refs.chatContainer.scrollHeight;
      });
    }
  }
};
</script>

<style scoped>
.chatUser {
  background-color: aqua;
}
.chatContainer {
  height: 400px;
  overflow-y: auto;
}
@keyframes slideIn {
  from {
    transform: translateX(0);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}
.spanMsg{
  border-radius: 15px;
  word-wrap: break-word;
  overflow-wrap: break-word;
  animation: slideIn 0.7s ease;
}
.nombreUsuario{
  animation: slideIn 0.7s ease;
}
</style>



