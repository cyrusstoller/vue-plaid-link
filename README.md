# vue-plaid-link

This package helps you to jump start the process of building a Vue.js application
that interacts with [Plaid](https://plaid.com).

To learn more about how to get started, check out the
[Plaid quickstart guide](https://plaid.com/docs/quickstart/).

## Installation

### npm

```
npm install --save vue-plaid-link
```

### yarn

```
yarn add vue-plaid-link
```

## Usage

```vue
<script>
import vue from 'vue';
import PlaidLink from 'vue-plaid-link';

vue.component('PlaidLink', PlaidLink);

export default {
  name: 'App',
  methods: {
    onLoad() {},
    onSuccess(public_token, metadata) {},
    onExit(err, metadata) {},
    onEvent(eventName, metadata) {}
  }
};
</script>

<template>
  <div id="app">
    <PlaidLink
      clientName="APPLICATION NAME"
      env="sandbox"
      public_key="PLAID PUBLIC KEY"
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
```

## Example

I have included an [example](https://github.com/cyrusstoller/vue-plaid-link/tree/master/example)
vue application that you can use to see how things work.

## Contributing

### Bugs / Issues

If you find a bug or something that could improve the user experience, please file an issue on this github project, so
contributors/maintainers can get started fixing them. :-)

### Submitting Pull Requests

- Fork this project
- Make a feature branch git checkout -b feature
- Make your changes and commit them to your feature branch
- Submit a pull request
