<template>
  <q-page class="flex flex-center">
    <AuthCard title="Регистрация">
      <q-form @submit="onSubmit" class="q-gutter-md">
        <q-input
          v-model="name"
          label="Имя"
          outlined
          :rules="[val => !!val || 'Имя обязательно']"
        />

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

        <q-input
          v-model="confirmPassword"
          label="Подтвердите пароль"
          :type="isPwd ? 'password' : 'text'"
          outlined
          :rules="[
            val => !!val || 'Подтверждение пароля обязательно',
            val => val === password || 'Пароли не совпадают'
          ]"
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
            label="Зарегистрироваться"
            type="submit"
            color="primary"
            class="full-width"
          />
        </div>
      </q-form>

      <SocialAuthButtons
        action="зарегистрироваться"
        @google-click="registerWithGoogle"
        @vk-click="registerWithVK"
      />

      <div class="text-center q-pt-md">
        Уже есть аккаунт?
        <router-link to="/login" class="text-primary">
          Войти
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

const name = ref('')
const email = ref('')
const password = ref('')
const confirmPassword = ref('')
const isPwd = ref(true)

const registerWithGoogle = () => {
  $q.notify({
    message: 'Функция регистрации через Google будет добавлена позже',
    color: 'info'
  })
}

const registerWithVK = () => {
  $q.notify({
    message: 'Функция регистрации через VK будет добавлена позже',
    color: 'info'
  })
}

const onSubmit = () => {
  // Here will be registration logic
  $q.notify({
    message: 'Функция регистрации будет добавлена позже',
    color: 'info'
  })
}
</script>

<style lang="scss" scoped>
.register-card {
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
