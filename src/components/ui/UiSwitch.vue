<template>
  <div class="ui-switch">
    <div class="ui-switch__field" @click="toggleValue">
      <span
        class="ui-switch__slider"
        :class="{
          'ui-switch__slider--active': value,
        }"
      />

      <span class="ui-switch__label">{{ label }}</span>
    </div>

    <p v-if="description" class="ui-switch__description">{{ description }}</p>
  </div>
</template>

<script>
export default {
  name: 'UiSwitch',

  props: {
    value: {
      type: Number,
      default: 0,
    },

    label: {
      type: String,
      default: '',
    },

    description: {
      type: String,
      default: '',
    },
  },

  methods: {
    toggleValue() {
      this.$emit('input', Number(!this.value));
    },
  },
};
</script>

<style lang="scss" scoped>
.ui-switch {
  display: flex;
  flex-direction: column;
  align-items: flex-start;

  &__field {
    display: flex;
    align-items: center;
    cursor: pointer;
    user-select: none;

    &:hover {
      .ui-switch__label {
        color: #7d7aff;
      }
    }
  }

  &__slider {
    position: relative;
    width: 39px;
    height: 19px;
    border-radius: 10px;
    background-color: #cdced8;
    transition: background-color .2s;

    &::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      background-color: #fff;
      border: 1px solid #cdced8;
      width: 19px;
      height: 19px;
      border-radius: 50%;
      transition: left .2s;
    }

    &--active {
      background-color: #7d7aff;

      &::before {
        left: 20px;
      }
    }
  }

  &__label {
    margin-left: 15px;
    font-weight: 500;
    line-height: 19px;
    transition: color .2s;
  }

  &__description {
    margin-top: 15px;
    font-size: 14px;
    line-height: 19px;
    letter-spacing: -0.021px;
    color: #696977;
  }
}
</style>
