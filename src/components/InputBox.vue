<template>
  <div id="input-box">
    <textarea v-model="inputValue" placeholder="Ctrl+Enter发送" v-on:keyup.ctrl.enter="send()"></textarea>
    <button type="button" @click="send()">发送</button>
  </div>
</template>

<script>
import { EventBus } from './../utils/EventBus';

export default {
  name: 'InputBox',
  props: ['ws'],
  data() {
    return {
      inputValue: ''
    }
  },
  methods: {
    send: function() {
      this.ws.send(this.inputValue);
      this.inputValue = '';
      EventBus.$emit('refresh');
    }
  },
  mounted() {
    EventBus.$on('itemClick', text => {
      this.inputValue = `${this.inputValue} ${text}`;
    })
  }
}
</script>

<style scoped>
#input-box {
  position: relative;
}

textarea {
  border: 1px solid #dedede;
  border-radius: 50px;
  padding: 10px 145px 10px 45px;
  outline: none;
  width: 100%;
  box-sizing: border-box;
  resize: none;
  font-size: 16px;
  color: #2c3e50;
  min-height: 100px;
}

textarea:focus {
  border-color: #42b983;
}

button {
  background-color: #42b983;
  color: white;
  cursor: pointer;
  padding: 14px;
  outline: none;
  border: none;
  border-radius: 40px;
  width: 100px;
  position: absolute;
  bottom: 4px;
  right: 30px;
}
</style>