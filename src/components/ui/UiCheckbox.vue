<template>
  <label class="ui-checkbox">
    <input
      type="checkbox"
      class="ui-checkbox__input"
      :checked="value"
      @change="onChange"
    >

    <span class="ui-checkbox__checkbox" />

    <span class="ui-checkbox__label">{{ label }}</span>
  </label>
</template>

<script>
export default {
  name: 'UiCheckbox',

  props: {
    value: {
      type: Boolean,
    },

    label: {
      type: String,
      default: '',
    },
  },

  methods: {
    onChange(e) {
      this.$emit('input', e.target.checked);
    },
  },
};
</script>

<style lang="scss" scoped>
.ui-checkbox {
  display: flex;
  align-items: flex-start;

  &__input {
    display: none;

    &:checked {
      + .ui-checkbox__checkbox {
        background-image: url("data:image/svg+xml,%3Csvg width='20' height='20' viewBox='0 0 20 20' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M5 10.5L8.00084 13L14 8' stroke='black' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E%0A");
        background-position: 0 -1px;
      }
    }
  }

  &__checkbox {
    flex-shrink: 0;
    width: 19px;
    height: 19px;
    background-color: #ffd467;
    border-radius: 5px;
    cursor: pointer;
  }

  &__label {
    margin-left: 15px;
    font-size: 14px;
    line-height: 19px;
    letter-spacing: -0.021px;
    user-select: none;
    cursor: pointer;
  }
}
</style>
