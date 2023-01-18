<script setup lang="ts">
import { reactive, ref, watch } from 'vue';
import { RouterLink, RouterView } from 'vue-router'
import StatusBar from './components/StatusBar.vue'

import { pb } from './pocketbase'

</script>

<template>
  <RouterView :pb="pb" />
  <StatusBar :pb="pb" />
</template>

<style scoped>

</style>
