<template>
  <q-page class="flex flex-center">
    <AuthCard title="Вход">
      <q-form @submit="onSubmit" class="q-gutter-md">
        <q-input
          v-model="email"
          label="Email"
          type="email"
          outlined
          :rules="[val => !!val || 'Email обязателен',
                  val => /.+@.+\..+/.test(val) || 'Введите корректный email']"
        />

        <q-input
          v-model="password"
          label="Пароль"
          :type="isPwd ? 'password' : 'text'"
          outlined
          :rules="[val => !!val || 'Пароль обязателен',
                  val => val.length >= 6 || 'Минимум 6 символов']"
        >
          <template v-slot:append>
            <q-icon
              :name="isPwd ? 'visibility_off' : 'visibility'"
              class="cursor-pointer"
              @click="isPwd = !isPwd"
            />
          </template>
        </q-input>

        <div class="full-width q-pt-md">
          <q-btn
            label="Войти"
            type="submit"
            color="primary"
            class="full-width"
          />
        </div>
      </q-form>

      <SocialAuthButtons
        action="войти"
        @google-click="loginWithGoogle"
        @vk-click="loginWithVK"
      />

      <div class="text-center q-pt-md">
        Нет аккаунта?
        <router-link to="/register" class="text-primary">
          Зарегистрироваться
        </router-link>
      </div>
    </AuthCard>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useQuasar } from 'quasar'
import AuthCard from 'components/AuthCard.vue'
import SocialAuthButtons from 'components/SocialAuthButtons.vue'

const router = useRouter()
const $q = useQuasar()

const email = ref('')
const password = ref('')
const isPwd = ref(true)

const loginWithGoogle = () => {
  $q.notify({
    message: 'Функция входа через Google будет добавлена позже',
    color: 'info'
  })
}

const loginWithVK = () => {
  $q.notify({
    message: 'Функция входа через VK будет добавлена позже',
    color: 'info'
  })
}

const onSubmit = () => {
  // Here will be login logic
  $q.notify({
    message: 'Функция входа будет добавлена позже',
    color: 'info'
  })
}
</script>

<style lang="scss" scoped>
.login-card {
  width: 100%;
  max-width: 400px;
  padding: 20px;
  border: 2px solid var(--q-primary);

  &.q-card--dark {
    border-color: var(--q-primary);
    box-shadow: 0 1px 5px rgba(var(--q-primary), 0.2),
                0 2px 2px rgba(var(--q-primary), 0.14),
                0 3px 1px -2px rgba(var(--q-primary), 0.12);
  }
}

.social-btn {
  width: 140px;
}
</style>
