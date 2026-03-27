<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

const name = ref("");
const email = ref("");
const password = ref("");

const register = async () => {
  const res = await fetch("https://auth-project-8157.onrender.com/register", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({
      name: name.value,
      email: email.value,
      password: password.value
    })
  });

  const data = await res.json();

  if (data) {
    alert("Registered successfully");
    router.push("/login"); // 👉 login page pe bhej do
  }
};
</script>

<template>
  <div style="padding:20px">
    <h2>Register</h2>

    <input v-model="name" placeholder="Name" /><br /><br />
    <input v-model="email" placeholder="Email" /><br /><br />
    <input v-model="password" type="password" placeholder="Password" /><br /><br />

    <button @click="register">Register</button>

    <br /><br />
    <button @click="$router.push('/login')">Go to Login</button>
  </div>
</template>