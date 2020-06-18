<template>
  <div id="app">
    <PlaidLink
      clientName="Vue Test"
      env="sandbox"
      public_key="dbaef5e48f1ccc027c209c029ef395"
      :products="['auth','transactions']"
      webhook="https://requestb.in"
      :onLoad='onLoad'
      :onSuccess='onSuccess'
      :onExit='onExit'
      :onEvent='onEvent'
      >
      <button>Open Link Slot</button>
    </PlaidLink>
  </div>
</template>

<script>
/* eslint-disable */
import PlaidLink from 'vue-plaid-link2'

export default {
  name: 'app',
  components: {
    PlaidLink
  },
  methods: {
    onLoad() {},
    onSuccess(public_token, metadata) {},
    onExit(err, metadata) {},
    onEvent(eventName, metadata) {}
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
