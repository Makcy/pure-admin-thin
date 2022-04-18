<script setup lang="ts">
import { reactive } from "vue";
import { useRouter } from "vue-router";
import { initRouter } from "/@/router/utils";
import { storageSession } from "/@/utils/storage";

const router = useRouter();

const loginForm = reactive({
  username: "admin",
  password: "123456"
});

const motionInitial = {
  opacity: 0,
  y: 100
};

const motionEnter = delay => ({
  opacity: 1,
  y: 0,
  transition: {
    delay
  }
});

const onLogin = (): void => {
  storageSession.setItem("info", {
    username: "admin",
    accessToken: "eyJhbGciOiJIUzUxMiJ9.test"
  });
  initRouter("admin").then(() => {});
  router.push("/");
};
</script>

<template>
  <div class="login-container">
    <el-form :model="loginForm" class="login-form">
      <h2 v-motion :initial="motionInitial" :enter="motionEnter(100)">
        Admin Template
      </h2>
      <el-form-item
        prop="username"
        v-motion
        :initial="motionInitial"
        :enter="motionEnter(200)"
      >
        <el-input v-model="loginForm.username" autocomplete="off" />
      </el-form-item>
      <el-form-item
        prop="password"
        v-motion
        :initial="motionInitial"
        :enter="motionEnter(300)"
      >
        <el-input
          v-model="loginForm.password"
          type="password"
          autocomplete="off"
        />
      </el-form-item>
      <el-form-item v-motion :initial="motionInitial" :enter="motionEnter(400)">
        <el-button style="width: 100%" type="primary" @click="onLogin"
          >登 录</el-button
        >
      </el-form-item>
    </el-form>
  </div>
</template>

<style scoped>
@import url("/@/style/login.css");
</style>
