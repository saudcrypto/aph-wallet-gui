<template>
  <modal-wrapper id="aph-send-with-ledger-modal">
    <div class="body">{{ prompt }}</div>
    <div class="footer">
      <div class="cancel-btn" @click="cancel">Cancel</div>
    </div>
  </modal-wrapper>
</template>

<script>
import ModalWrapper from './ModalWrapper';
export default {
  components: {
    ModalWrapper,
  },

  computed: {
    prompt() {
      if (this.$store.state.showSendRequestLedgerSignature === true) {
        return 'Please confirm the transaction on your Ledger device.';
      }

      return 'Please connect your Ledger device, unlock it and open the NEO application.';
    },
  },

  methods: {
    cancel() {
      this.$services.ledger.close();
      this.$store.commit('setSendInProgress', false);
      this.$store.commit('setShowSendWithLedgerModal', false);
    },
  },
};
</script>


<style lang="scss">
#aph-send-with-ledger-modal {
  .body {
    padding: $space-xl;
    text-align: center;
    display: block;
  }


  .footer {
    display: flex;

    > * {
      flex: 1;
    }
  }

  .cancel-btn {
    @extend %btn-footer-light;
  }

  .login-btn {
    @extend %btn-footer;
  }
}
</style>

