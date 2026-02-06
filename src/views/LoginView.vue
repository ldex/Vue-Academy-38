<template>
  <div style="margin-bottom: 80px">
        <h2>Login</h2>
        <form @submit.prevent="login">
            <input label="Username" type="text" name="username" v-model="username" required autofocus
                autocomplete="off" />
            <br />
            <input label="Password" type="password" name="password" required v-model="password" />
            <br />
            <button type="submit">Login</button>
        </form>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { useUserStore } from '@/stores/user';

const userStore = useUserStore();
const router = useRouter()

const username = ref<string>('')
const password = ref<string>('')

async function login(): Promise<void> {
    try {
        await userStore.login({
            username: username.value,
            password: password.value
        })
        router.push({ name: "admin" });
        console.log('Successfully logged in!');
    } catch (error) {
        console.error('Login failed: ', error);
    }
}
</script>

<style scoped></style>