<template>
  <div>
    <p v-if="isConnected">We're connected to the server!</p>
    <p>Message from server: "{{ socketMessage }}"</p>
    <button @click="pingServer()">Ping Server</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isConnected: false,
      socketMessage: ""
    };
  },
  sockets: {
    connect() {
      // Fired when the socket connects.
      this.isConnected = true;
    },
    disconnect() {
      this.isConnected = false;
    },
    messageChannel(data) {
      this.socketMessage = data;
    }
  },
  methods: {
    pingServer() {
      // Send the "pingServer" event to the server.
      this.$socket.emit("pingServer", "PING!");
    }
  }
};
</script>
