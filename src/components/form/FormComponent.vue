<template>
  <form class="form">
    <div class="form__head">
      <p class="form__title">Регистрация</p>
    </div>

    <div class="form__body">
      <FormBlock class="form__block">
        <UiSwitch
          v-model="values.public"
          label="Публичный профиль"
          description="Включает профиль для просмотра другими пользователями по ссылке"
        />
      </FormBlock>

      <FormBlock title="Данные" class="form__block">
        <div class="form__fields-grid">
          <UiInput
            v-model="values.username"
            class="form__field"
            placeholder="Имя"
            :error="errors.username"
            @input="onInput('username')"
          />

          <UiSelect
            v-model="values.role"
            class="form__field"
            :options="[
              {value: 0, name: 'Разработчик'},
              {value: 1, name: 'Дизайнер'},
              {value: 2, name: 'Тестировщик'},
              {value: 3, name: 'Менеджер'},
            ]"
            placeholder="Должность"
          />

          <UiInput
            v-model="values.email"
            class="form__field"
            placeholder="Email"
            :error="errors.email"
            @input="onInput('email')"
          />

          <UiInput
            v-model="values.password"
            class="form__field form__field--password"
            type="password"
            placeholder="Пароль"
            :error="errors.password"
            @input="onInput('password')"
          />

          <UiInput
            v-model="values.password_repeat"
            class="form__field"
            type="password"
            placeholder="Повторите пароль"
            :error="errors.password_repeat"
            @input="onInput('password_repeat')"
          />
        </div>
      </FormBlock>

      <div class="form__consent-checkbox">
        <UiCheckbox
          v-model="isConsentConfirmed"
          :label="consentLabel"
        />
      </div>

      <div class="form__button-wrap">
        <UiButton
          class="form__button"
          :disabled="isButtonDisabled"
          @click.native="submitForm"
        >Регистрация</UiButton>
      </div>
    </div>
  </form>
</template>

<script>
import FormBlock from '@/components/form/FormBlock.vue';
import UiSwitch from '@/components/ui/UiSwitch.vue';
import UiInput from '@/components/ui/UiInput.vue';
import UiSelect from '@/components/ui/UiSelect.vue';
import UiCheckbox from '@/components/ui/UiCheckbox.vue';
import UiButton from '@/components/ui/UiButton.vue';

export default {
  name: 'FormComponent',

  components: {
    FormBlock,
    UiSwitch,
    UiInput,
    UiSelect,
    UiCheckbox,
    UiButton,
  },

  props: {
    defaultValues: {
      type: Object,
      default: () => ({}),
    },
  },

  data() {
    return {
      values: {
        public: 0,
        username: '',
        role: null,
        email: '',
        password: '',
        password_repeat: '',
        ...this.defaultValues,
      },

      errors: {},

      isConsentConfirmed: true,
      consentLabel: 'Нажимая на кнопку “Регистрация”, я подтверждаю свое согласение с политикой конфиденциальности и обработки персональных данных',

      isWaitResponse: false,
    };
  },

  computed: {
    isButtonDisabled() {
      return !this.isConsentConfirmed
        || this.isWaitResponse
        || Object.keys(this.errors).length > 0;
    },
  },

  methods: {
    async submitForm() {
      if (this.isButtonDisabled) {
        return;
      }

      try {
        this.isWaitResponse = true;
        const response = await fetch('https://lmstestapi.reezonly.com/v1/user/signup', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json;charset=utf-8',
          },
          body: JSON.stringify(this.values),
        });

        const { success, errors } = await response.json();

        if (success) {
          this.$emit('success');
        } else {
          this.setErrors(errors);
        }
      } catch (err) {
        // eslint-disable-next-line no-console
        console.warn('[FormComponent/submitForm] failed: ', err);
      } finally {
        this.isWaitResponse = false;
      }
    },

    setErrors(errors) {
      const newErrors = {};

      Object.entries(errors).forEach(([name, value]) => {
        newErrors[name] = value.join(' ');
      });

      this.errors = newErrors;
    },

    onInput(name) {
      this.$delete(this.errors, name);
    },
  },
};
</script>

<style lang="scss" scoped>
.form {
  border-radius: 15px;
  background-color: #fff;

  &__head {
    padding: 27px 20px;
    border-bottom: 1px solid #edeff3;
  }

  &__title {
    font-size: 19px;
    font-weight: 700;
    line-height: 27px;
    letter-spacing: -0.066px;
  }

  &__body {
    padding: 27px 20px 45px;
  }

  &__block {
    margin-top: 20px;

    &:first-child {
      margin-top: 0;
    }
  }

  &__fields-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 25px 18px;

    @media (max-width: 767.98px) {
      grid-template-columns: 1fr;
    }
  }

  &__field {
    &--password {
      grid-column: 1;
    }
  }

  &__consent-checkbox {
    margin-top: 25px;
    max-width: 716px;
  }

  &__button-wrap {
    margin-top: 40px;
    display: flex;
    justify-content: center;
  }

  &__button {
    width: 210px;
  }
}
</style>
