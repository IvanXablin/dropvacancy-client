<script setup lang="ts">
import { ref } from 'vue';
import type { TUser }  from '@/types/TUser';
import { useRouter } from 'vue-router';
import { authApi } from '@/api/auth.api';

const nameInput = ref('');
const emailInput = ref('');
const passwordInput = ref('');
const confirmPasswordInput = ref('');

const router = useRouter();

const handleRegister = async ():Promise<void> => {

  if (!validateForm()) return;

  const user:TUser = {
    name: nameInput.value,
    email: emailInput.value,
    password: passwordInput.value,
  };

  const [error, response] = await authApi.register(user);

  if (error) {
    alert(`Произошла ошибка, попробуйте зарегистрироваться еще раз\n\nОшибка: ${ error.message }` );
    return;
  }
  if (response) {
    alert("Вы вошли");

    setTimeout(async () => {
      await router.push({ path: '/account' });
    }, 1000);
  }
};

const validateForm = ():boolean => {

  if (!nameInput.value) return false;

  if (nameInput.value.length > 40) return false;

  if (!emailInput.value) return false;

  if (!passwordInput.value) return false;

  if (passwordInput.value !== confirmPasswordInput.value) return false;

  return true;
};
</script>

<template>
  <div class="regist-form">
    <el-input
        v-model="nameInput"
        placeholder="Ваше имя"
    />
    <el-input
        v-model="emailInput"
        placeholder="Ваша почта"
    />
    <el-input
        v-model="passwordInput"
        type="password"
        placeholder="Пароль"
        show-password
    />
    <el-input
        v-model="confirmPasswordInput"
        type="password"
        placeholder="Повторите пароль"
        show-password
    />
    <el-button @click="handleRegister" type="primary" round>Зарегистрироваться</el-button>
  </div>
</template>

<style lang="scss" scoped>
.regist-form {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  width: 100%;
  height: 90%;
}
</style>