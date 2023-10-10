<template>
  <div class="form-block">
    <p v-if="title" class="form-block__title">{{ title }}</p>
    <slot />
  </div>
</template>

<script>
export default {
  name: 'FormBlock',

  props: {
    title: {
      type: String,
      default: '',
    },
  },
};
</script>

<style lang="scss" scoped>
.form-block {
  padding-bottom: 30px;
  border-bottom: 1px solid #d9d9d9;

  &__title {
    margin-bottom: 25px;
    font-size: 16px;
    font-weight: 500;
    line-height: 19px;
  }
}
</style>
