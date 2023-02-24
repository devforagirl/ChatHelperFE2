<template>
  <div>
    <h1>Chat Helper T</h1>
    <div v-if="!socketConnected">
      <button @click="connectSocket">Connect</button>
    </div>
    <div v-else>
      <button @click="disconnectSocket">Disconnect</button>
    </div>

    <div>
      <button @click="btnClick1">btnClick1</button>
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
      console.log('process.env.VUE_APP_BACKEND_URL T->', process.env.VUE_APP_BACKEND_URL)
      this.socket = io(process.env.VUE_APP_BACKEND_URL)
      this.socket.on('connect', () => {
        console.log('Connected to server')
        this.socketConnected = true
      })

      this.socket.on('response', () => {
        console.log('response +1')
      })
    },
    disconnectSocket() {
      this.socket.disconnect()
      this.socketConnected = false
      console.log('Disconnected from server')
    },

    btnClick1(){
      console.log('btnClick1')
      this.socket.emit('message','btnClick1')
    }
  },
}
</script>
