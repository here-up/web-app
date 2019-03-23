<template>
  <a-form>
    <a-input v-model.trim="newAccountName"/>
    <a-input v-model.trim="ownerPublicKey"/>
    <a-input v-model.trim="activePublicKey"/>
    <a-button type="primary">Join</a-button>
  </a-form>
</template>

<script>
  import { Form, Button, Input } from 'ant-design-vue';

  export default {
    name: 'join-form',
    data() {
      return {
        newAccountName: '',
        ownerPublicKey: '',
        activePublicKey: '',
      };
    },
    components: {
      AForm: Form,
      AButton: Button,
      AInput: Input,
    },
  };
</script>

<style lang="scss" scoped>
  //
</style>

