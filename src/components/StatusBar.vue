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
  <div id="status-bar">
    <p class="item logged-in" v-if="state.loggedIn">Logged in as: <span>{{ state.username || "none" }}</span></p>
    <p class="item not-logged-in" v-else>Not logged in</p>
  </div>
</template>

<style scoped>
#status-bar {
  position: absolute;
  left: 0;
  bottom: 0;
  background: #222;
  border-top: 1px #444 solid;
  width: 100%;
  height: 40px;
  z-index: 2;

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

#status-bar .item {
  display: inline-block;
  margin: 0;
  font-size: 12px;

  border-radius: 32px;
  border: solid 1px #444;
  padding: 2px 8px;
}

#status-bar .logged-in {
  color: #004;
  background: #88F;
  padding: 2px 2px;
  padding-left: 12px;
  display: flex;
  align-items: center;
}

#status-bar .logged-in span {
  display: inline-block;
  color: #AAF;
  background: #222;
  border-radius: 32px;
  padding: 2px 8px;
  margin-left: 4px;
}
</style>
