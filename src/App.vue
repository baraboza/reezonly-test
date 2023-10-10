<template>
  <div class="container">
    <transition name="fade" mode="out-in">
      <FormComponent
        v-if="!isFormSuccess"
        :default-values="defaultValues"
        @success="isFormSuccess = true"
      />

      <SuccessAlert v-else>
        Регистрация успешно завершена
      </SuccessAlert>
    </transition>
  </div>
</template>

<script>
import FormComponent from '@/components/form/FormComponent.vue';
import SuccessAlert from '@/components/SuccessAlert.vue';

export default {
  name: 'App',
  components: {
    FormComponent,
    SuccessAlert,
  },

  data() {
    return {
      defaultValues: {
        public: 1,
        username: 'default username',
        email: 'default email',
      },

      isFormSuccess: false,
    };
  },
};
</script>

<style lang="scss" scoped>
@import url("@/assets/scss/app.scss");

.container {
  width: 100%;
  max-width: 958px;
  margin: 50px auto;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .3s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
