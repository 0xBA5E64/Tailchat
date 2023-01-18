<script setup lang="ts">

</script>

<template>
  <div>
    <h1>This is the Statusbar</h1>
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
