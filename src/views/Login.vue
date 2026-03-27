<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

const email = ref("");
const password = ref("");

const login = async () => {
  const res = await fetch("https://auth-project-8157.onrender.com/login", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({
      email: email.value,
      password: password.value
    })
  });

  const data = await res.json();

  if (data.token) {
    localStorage.setItem("token", data.token);
    router.push("/dashboard");
  } else {
    alert("Login failed");
  }
};
</script>

<template>
  <div>
    <h2>Login</h2>
    <input v-model="email" placeholder="Email" /><br><br>
    <input v-model="password" type="password" placeholder="Password" /><br><br>
    <button @click="login">Login</button>
  </div>
</template>