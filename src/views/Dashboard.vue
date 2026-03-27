<script setup lang="ts">
import { useRouter } from "vue-router";
import { ref, onMounted } from "vue";

const router = useRouter();

const logout = () => {
    localStorage.removeItem("token");
    router.push("/");
};

type User = {
  id: number;
  name: string;
  email: string;
};

const users = ref<User[]>([]);

const getusers = async () => {
    const res = await fetch("https://auth-project-8157.onrender.com/users");
    const data = await res.json();
    users.value = data;
}
onMounted(() => {
    getusers();
});
</script>

<template>
    <div>
        <h2>Dashboard</h2>
        <p>Login Success 🎉</p>
        <button @click="logout">Logout</button>
    </div>
    <div style="padding:20px">
        <h2>All Users</h2>

        <table border="1" cellpadding="10">
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Email</th>
            </tr>

            <tr v-for="user in users" :key="user.id">
                <td>{{ user.id }}</td>
                <td>{{ user.name }}</td>
                <td>{{ user.email }}</td>
            </tr>
        </table>
    </div>
</template>