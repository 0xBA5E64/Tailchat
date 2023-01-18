<script setup lang="ts">
import { ref, reactive } from 'vue'
import PocketBase from 'pocketbase'

const props = defineProps({
  pb: { type: PocketBase, required: true }
})

const username = ref('');
const password = ref('');

function login_user() {
  props.pb.collection('users').authWithPassword(username.value, password.value);
}

function logout_user() {
  props.pb.authStore.clear();
}

interface state {
  loggedIn: boolean,
  username: string
}

const state = reactive({
  loggedIn: props.pb.authStore.isValid,
  username: props.pb.authStore.model?.username || "Unregistered"
})

props.pb.authStore.onChange(()=>{
  state.loggedIn = props.pb.authStore.isValid;
  state.username = props.pb.authStore.model?.username || "Unregistered";
})

</script>

<template>
  <div>
    <form v-if="!state.loggedIn" @submit.prevent="login_user">
      <h1>Welcome Back</h1>
      <input v-model="username" type="text">
      <input v-model="password" type="password">
      <button>Log in?</button>
    </form>
    <div v-else>
      <h1>Currently logged in as: {{ state.username }}</h1>
      <button @click="logout_user">Logout</button>
    </div>
  </div>
</template>

<style scoped>

</style>
