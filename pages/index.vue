<template>
  <b-container class="py-5">
    <h1>So simple chat</h1>

    <p>
      Type message and press ENTER to send message.
    </p>

    <b-textarea v-model="chat" rows="10" readonly no-resize></b-textarea>

    <b-row class="mt-3">
      <b-col cols="3">
        <b-input v-model="nick" class="w-100"></b-input>
      </b-col>
      <b-col cols="9">
        <b-input v-model="msg" ref="msg" class="w-100" @keydown.enter="send"></b-input>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>

export default {
  data () {
    return {
      chat: '',
      nick: 'Nick',
      msg: '',
      ws: null,
    }
  },
  methods: {
    send () {
      this.ws.send(`${this.nick}: ${this.msg}`)
      this.msg = ''
    },
  },
  mounted () {
    this.$refs.msg.focus()
    this.ws = new WebSocket(`ws://${document.location.host}/chat`)
    this.ws.onmessage = ev => this.chat += `${ev.data}\n`
  },
}
</script>
