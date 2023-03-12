<template>
  <div>
    <h1>Chat Helper T</h1>
    <div v-if="!socketConnected">
      <button @click="connectSocket">Connect</button>
    </div>
    <div v-else>
      <button @click="disconnectSocket">Disconnect</button>
    </div>

    <br />
    <div>
      <button @click="btnClick1">message</button>
    </div>
    <br />
    <div>
      <button @click="btnClick2">startProcess</button>
    </div>
    <br />
    <div>
      <button @click="btnClick2">createChatObject</button>
    </div>
    <br />
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

      this.socket.on('chatsData', (r) => {
        console.log('chatsData +1', r)
      })

      this.socket.on('exceptionInfo', (e) => {
        console.log('exceptionInfo +1', e)
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
    },
    btnClick2(){
      console.log('btnClick2')
      this.socket.emit('startProcess')
    },
    btnClick3(){
       console.log('btnClick3')
  this.socket.emit('createChatObject', (fb) => {
    console.log('fb:', fb)
  })
    }
  }
}
</script>
