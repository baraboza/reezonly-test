<template>
  <div class="ui-select">
    <select class="ui-select__select" @change="onChange">
      <option value="" disabled selected>{{ placeholder }}</option>

      <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
        :selected="option.value === value"
      >{{ option.name }}</option>
    </select>

    <svg class="ui-select__arrow" width="19" height="19" viewBox="0 0 19 19" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M13 9L9.5 12L6 9" stroke="#A7A7B6" stroke-width="1.5" stroke-linecap="round"
            stroke-linejoin="round"/>
    </svg>
  </div>
</template>

<script>
export default {
  name: 'UiSelect',

  props: {
    value: {
      type: [String, Number],
      default: '',
    },

    options: {
      type: Array,
      default: () => [],
    },

    placeholder: {
      type: String,
      default: '',
    },
  },

  methods: {
    onChange(e) {
      this.$emit('input', this.options[e.target.selectedIndex - 1].value);
    },
  },
};
</script>

<style lang="scss" scoped>
.ui-select {
  position: relative;

  &__select {
    width: 100%;
    padding: 0 9px;
    border: 1px solid #e6e6eb;
    border-radius: 11px;
    font-size: 14px;
    letter-spacing: -0.021px;
    height: 39px;
    appearance: none;
    cursor: pointer;
  }

  &__arrow {
    position: absolute;
    top: 10px;
    right: 12px;
  }
}
</style>
