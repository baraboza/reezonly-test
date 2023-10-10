<template>
  <div class="ui-input">
    <input
      class="ui-input__input"
      :type="type"
      :value="value"
      :placeholder="placeholder"
      @input="onInput"
    >

    <p v-if="error" class="ui-input__error">{{ error }}</p>
  </div>
</template>

<script>
export default {
  name: 'UiInput',

  props: {
    value: {
      type: String,
      default: '',
    },

    type: {
      type: String,
      default: 'text',
      validator: (value) => ['text', 'password'].includes(value),
    },

    placeholder: {
      type: String,
      default: '',
    },

    error: {
      type: String,
      default: '',
    },
  },

  methods: {
    onInput(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.ui-input {
  &__input {
    width: 100%;
    padding: 0 9px;
    border: 1px solid #e6e6eb;
    border-radius: 11px;
    background-color: #fff;
    font-size: 14px;
    letter-spacing: -0.021px;
    height: 39px;

    &::placeholder {
      color: #9292a0;
    }
  }

  &__error {
    margin-top: 8px;
    font-size: 12px;
    line-height: 14px;
    color: red;
  }
}
</style>
