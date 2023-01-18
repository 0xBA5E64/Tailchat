<script setup lang="ts">
import { reactive, ref, watch } from 'vue';
import { RouterLink, RouterView } from 'vue-router'
import StatusBar from './components/StatusBar.vue'

import { pb } from './pocketbase'
const rpb = reactive(pb);

</script>

<template>
  <RouterView :pb="rpb" />
  <StatusBar :pb="rpb" />
</template>

<style scoped>

</style>
