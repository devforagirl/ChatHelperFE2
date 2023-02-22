<template>
  <div>
    <h1>Chat Helper i</h1>
    <div v-if="!socketConnected">
      <button @click="connectSocket">Connect</button>
    </div>
    <div v-else>
      <button @click="disconnectSocket">Disconnect</button>
    </div>
  </div>
</template>

<script>
import io from 'socket.io-client'

export default {
  name: 'HomeView',
  components: {
  },
  data() {
    return {
      socketConnected: false,
    }
  },
  methods: {
    connectSocket() {
      console.log('process.env.VUE_APP_BACKEND_URL e->', process.env.VUE_APP_BACKEND_URL)
      this.socket = io(process.env.VUE_APP_BACKEND_URL)
      this.socket.on('connect', () => {
        console.log('Connected to server')
        this.socketConnected = true
      })
    },
    disconnectSocket() {
      this.socket.disconnect()
      this.socketConnected = false
      console.log('Disconnected from server')
    },
  },
}
</script>
