<template>
  <div>
    <h2>Register</h2>
    <form @submit.prevent="register">
      <input v-model="username" placeholder="Username" />
      <input v-model="password" type="password" placeholder="Password" />
      <button>Register</button>
    </form>
    <p>{{ error }}</p>
  </div>
</template>

<script>
import api from "@/api/axios";

export default {
  data() {
    return {
      username: "",
      password: "",
      error: "",
    };
  },
  methods: {
    async register() {
      try {
        await api.post("/api/auth/register", {
          username: this.username,
          password: this.password,
        });
        this.$router.push("/login");
      } catch (err) {
        this.error = "Registration failed";
      }
    },
  },
};
</script>
