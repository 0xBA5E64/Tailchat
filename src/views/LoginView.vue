<script setup lang="ts">
import { ref, reactive } from 'vue'
import PocketBase from 'pocketbase'

const props = defineProps({
  pb: { type: PocketBase, required: true }
})

const username = ref('');
const password = ref('');

let authData;

function login_user() {
  state.isLoading = true;
  authData = props.pb.collection('users').authWithPassword(username.value, password.value)
    .then(()=>{
      state.isLoading = false;
    })
    .catch((err)=>{
      state.errorMessage = err.data.message
      state.isLoading = false;
    });
  console.log(authData);
}

function logout_user() {
  props.pb.authStore.clear();
}

interface state {
  loggedIn: boolean,
  username: string,
  isLoading: boolean,
  errorMessage: string,
}

const state = reactive({
  loggedIn: props.pb.authStore.isValid,
  username: props.pb.authStore.model?.username || "Unregistered",
  isLoading: false,
  errorMessage: ""
})

props.pb.authStore.onChange(() => {
  state.loggedIn = props.pb.authStore.isValid;
  state.username = props.pb.authStore.model?.username || "Unregistered";
})

</script>

<template>
  <div class="page-wrapper">

    <div class="loading-overlay" :class="{active: state.isLoading}">
      <v-progress-circular indeterminate></v-progress-circular>
    </div>

    <v-card v-if="!state.loggedIn" variant="outlined" width="400">

      <v-form @submit.prevent="login_user">
        <v-card-title>
          <b>Welcome Back</b>
        </v-card-title>
        <v-card-subtitle>
          Please provide your login credentials
        </v-card-subtitle>

        <v-card-text>
          <v-text-field v-model="username" label="Username" variant="outlined">
          </v-text-field>

          <v-text-field v-model="password" label="Password" variant="outlined" type="password">
          </v-text-field>
          <p v-if="state.errorMessage != ''" class="text-red">{{state.errorMessage}}</p>
        </v-card-text>

        <v-card-actions>
          <v-btn variant="tonal" @click="login_user">
            Log In
          </v-btn>
        </v-card-actions>
      </v-form>
    </v-card>

    <div v-else>
      <h1>Currently logged in as: {{ state.username }}</h1>
      <v-btn variant="outlined" class="text-red" @click="logout_user">
        Logout
      </v-btn>
    </div>

  </div>
</template>

<style scoped>

.page-wrapper {
  width: 100%;
  height: 100%;

  display: flex;
  justify-content: center;
  align-items: center;
}

.loading-overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1;

  backdrop-filter: blur(8px);
  opacity: 0;
  visibility: hidden;

  display: flex;
  justify-content: center;
  align-items: center;

  transition: .5s;
}

.loading-overlay.active {
  visibility: visible;
  opacity: 1;
}

</style>
