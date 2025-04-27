<template>
  <div>
    <h2>Login</h2>
    <form @submit.prevent="login">
      <input v-model="username" placeholder="Username" />
      <input v-model="password" type="password" placeholder="Password" />
      <button>Login</button>
    </form>
    <p>{{ error }}</p>
  </div>
</template>

<script setup>
import { ref } from "vue";
import api from "@/api/axios";
import { useRouter } from "vue-router";
import { useAuthStore } from "@/stores/authStore";

const username = ref("");
const password = ref("");
const error = ref("");

const router = useRouter();
const auth = useAuthStore();

const login = async () => {
  try {
    const res = await api.post("/api/auth/login", {
      username: username.value,
      password: password.value,
    });

    auth.login(res.data.token, username.value); // Use actual username if returned
    router.push("/");
  } catch (err) {
    error.value = "Login failed";
  }
};
</script>
