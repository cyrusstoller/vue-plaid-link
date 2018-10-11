<template>
  <div @click="link_open" :style="{display: 'inline'}">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    clientName: String,
    env: {
      type: String,
      required: true,
      default: 'sandbox',
      validator: function (value) {
        // The value must match one of these strings
        return ['sandbox', 'development', 'production'].indexOf(value) !== -1
      }
    },
    public_key: String,
    products: Array,
    webhook: {
      type: String,
      required: false
    },
    onLoad: {
      type: Function,
      required: false
    },
    onSuccess: Function,
    onExit: {
      type: Function,
      required: false
    },
    onEvent: {
      type: Function,
      required: false
    }
  },
  data() {
    return {
      plaid: null
    }
  },
  methods: {
    link_open(e) {
      e.preventDefault()

      let self = this
      if (this.plaid != null) {
        this.plaid.create({
          clientName: this.clientName,
          env: this.env,
          key: this.public_key,
          product: this.products,
          // Optional – use webhooks to get transaction and error updates
          webhook: this.webhook,
          onLoad: function() {
            // Optional, called when Link loads
            self.onLoad()
          },
          onSuccess: function(public_token, metadata) {
            // Send the public_token to your app server.
            // The metadata object contains info about the institution the
            // user selected and the account ID or IDs, if the
            // Select Account view is enabled.
            self.onSuccess(public_token, metadata)
          },
          onExit: function(err, metadata) {
            // The user exited the Link flow.
            if (err != null) {
              // The user encountered a Plaid API error prior to exiting.
            }
            // metadata contains information about the institution
            // that the user selected and the most recent API request IDs.
            // Storing this information can be helpful for support.
            self.onExit(err, metadata)
          },
          onEvent: function(eventName, metadata) {
            // Optionally capture Link flow events, streamed through
            // this callback as your users connect an Item to Plaid.
            // For example:
            // eventName = "TRANSITION_VIEW"
            // metadata  = {
            //   link_session_id: "123-abc",
            //   mfa_type:        "questions",
            //   timestamp:       "2017-09-14T14:42:19.350Z",
            //   view_name:       "MFA",
            // }
            self.onEvent(eventName, metadata)
          }
        }).open()
      }
    }
  },
  mounted() {
    let linkScript = document.createElement('script')
    linkScript.async = true
    linkScript.setAttribute('src', 'https://cdn.plaid.com/link/v2/stable/link-initialize.js')
    document.head.appendChild(linkScript)

    linkScript.onload = () => {
      this.plaid = window.Plaid
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
