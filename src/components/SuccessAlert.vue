<template>
  <div class="success-alert">
    <div class="success-alert__circle">
      <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M5 10.5L8.00084 13L14 8"
              stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </div>

    <p class="success-alert__text">
      <slot></slot>
    </p>
  </div>
</template>

<script>
export default {
  name: 'SuccessAlert',
};
</script>

<style lang="scss" scoped>
.success-alert {
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 15px;
  background-color: #fff;
  padding: 100px 40px;
  text-align: center;

  &__circle {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 80px;
    height: 80px;
    border-radius: 50%;
    background-color: #07a86e;

    svg {
      width: 60px;
      height: 60px;
    }

    path {
      stroke: #fff;
    }
  }

  &__text {
    margin-top: 20px;
    font-size: 19px;
    font-weight: 700;
    line-height: 27px;
    letter-spacing: -0.066px;
  }
}
</style>
