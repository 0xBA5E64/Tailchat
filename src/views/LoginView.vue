<script setup lang="ts">
import { ref, reactive } from 'vue'

const props = defineProps(['pb'])

const username = ref('');
const password = ref('');

function login_user() {
  props.pb.collection('users').authWithPassword(username.value, password.value);
}

function logout_user() {
  props.pb.authStore.clear();
}

type state = {
  loggedIn: boolean,
  username: string
}

const state = reactive({
  loggedIn: props.pb?.authStore.isValid || false,
  username: props.pb?.authStore.model?.username || ""
})

props.pb?.authStore.onChange(()=>{
  state.loggedIn = props.pb?.authStore.isValid || false;
  state.username = props.pb?.authStore.model?.username;
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
