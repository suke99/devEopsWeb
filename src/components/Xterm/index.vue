<template>
  <div>
    <div ref="yoshell"></div>
  </div>
</template>

<script>
  import { Terminal } from 'xterm';
  import * as attach from 'xterm/lib/addons/attach/attach';
  import 'xterm/lib/xterm.css'
  export default {
    components: { Terminal },
    name: 'Xterm',
    props: {
      rows: {
        type: Number,
        default: 20
      },
      cols: {
        type: Number,
        default: 120
      },
      work_uuid:{
        type: String,
        default: ''
      }
    },
    data() {
      return {
        term: null,
        socket: null
      }
    },
    mounted(){
      Terminal.applyAddon(attach);
      this.term = new Terminal({
        rows: this.rows,
        cols: this.cols,
        screenKeys: true,
        useStyle: true,
        cursorBlink: true
      })
      this.term.open(this.$refs.yoshell,false)
      this.socket = new WebSocket('ws://'+ GLOBAL.API_URL+'/ansible/'+this.work_uuid+'/')
      this.term.attach(this.socket)
      this.term.focus()
    },
    beforeDestroy(){
      console.log('销毁操作')
      this.socket.close()
      this.term.destroy()
    }
  }
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
</style>
