<template>
  <div>
    <h1>Chat Helper 233</h1>
    <div v-if="!socketConnected">
      <button @click="connectSocket">Connect</button>
    </div>
    <div v-else>
      <button @click="disconnectSocket">Disconnect</button>
      <chat-room />
    </div>
  </div>
</template>

<script>
import io from 'socket.io-client';
// import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: 'HomeView',
  components: {
    // HelloWorld,
  },
  data() {
    return {
      socketConnected: false,
    };
  },
  methods: {
    connectSocket() {
      this.socket = io(process.env.VUE_APP_BACKEND_URL);
      this.socket.on('connect', () => {
        console.log('Connected to server');
        this.socketConnected = true;
      });
    },
    disconnectSocket() {
      this.socket.disconnect();
      this.socketConnected = false;
      console.log('Disconnected from server');
    },
  },
};
</script>
