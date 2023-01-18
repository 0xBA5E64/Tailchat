<script setup lang="ts">
import { reactive } from 'vue'

import PocketBase from 'pocketbase';
const props = defineProps({
  pb: { type: PocketBase, required: true }
})

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
    <h1 v-if="state.loggedIn">Logged in as: {{ state.username || "none" }}</h1>
    <h1 v-else>Not logged in</h1>
  </div>
</template>

<style scoped>
div {
  position: absolute;
  left: 0;
  bottom: 0;
  background: #222;
  border-top: 1px #444 solid;
  width: 100%;
  height: 40px;

  padding: 0 16px;
  box-sizing: border-box;

  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;

  color: #DDD;
  font-family: 'Roboto Mono', Courier, monospace;
  text-transform: uppercase;
}

div * {
  margin: 0;
  font-size: 12px;
}
</style>
