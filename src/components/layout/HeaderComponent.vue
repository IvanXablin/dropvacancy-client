<script setup lang="ts">
import { ref } from 'vue';
import 'element-plus/theme-chalk/display.css';

const drawer = ref(false);
const handleOpenMenu = (): void => {
  drawer.value = true;
}
</script>

<template>
<div class="header">
  <p class="header__logo">dropvacancy</p>
  <el-row :gutter="10" class="hidden-sm-and-down">
    <el-col :xs="4" :sm="6" :md="8" :lg="9" :xl="11">
      <div class="header__nav">
        <router-link class="header__link" to="/">Вакансии</router-link>
        <router-link class="header__link" to="/">Аналитика</router-link>
        <router-link class="header__link" to="/">О нас</router-link>
      </div>
    </el-col>
  </el-row>
  <el-row :gutter="10" class="hidden-md-and-up">
    <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="1">
      <el-icon size="30px" color="white" @click="handleOpenMenu">
        <Menu />
      </el-icon>
      <el-drawer v-model="drawer" :with-header="false" size="50%">
        <div class="menu">
          <router-link class="header__link" to="/">Вакансии</router-link>
          <router-link class="header__link" to="/">Аналитика</router-link>
          <router-link class="header__link" to="/">О нас</router-link>
        </div>
      </el-drawer>
    </el-col>
  </el-row>
</div>
</template>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: space-around;
  padding: 30px;
  box-shadow: 1px 1px rgba(70, 70, 70, 0.2);

  &__logo {
    font-size: 21px;
    font-weight: bold;
    text-transform: uppercase;
  }

  &__nav {
    display: flex;
    align-items: center;
  }

  &__link {
    margin: 0 15px;
    font-size: 16px;
    text-decoration: none;
    color: white;
    white-space: nowrap;

    &:hover {
      color: rgba(206, 71, 92, 0.85);
    }
  }
}
</style>