<template>
  <button class="ui-button" type="button">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'UiButton',
};
</script>

<style scoped>
.ui-button {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 39px;
  padding: 0 12px;
  border: 1px solid #07a86e;
  border-radius: 9px;
  font-size: 14px;
  line-height: 19px;
  letter-spacing: -0.021px;
  color: #07a86e;
  transition-property: background-color, color;
  transition-duration: .2s;

  &:hover:not(:disabled) {
    background-color: #07a86e;
    color: #fff;
  }

  &:disabled {
    opacity: 0.6;
    border-color: grey;
    color: grey;
    cursor: not-allowed;
  }
}
</style>
