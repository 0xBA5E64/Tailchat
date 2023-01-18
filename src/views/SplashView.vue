<script setup lang="ts">

</script>

<template>
  <main>
    <h1>Welcome to<br><span>TailChat.</span></h1>
    <div>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="login">Log In</RouterLink>
      <RouterLink to="chat">Chat</RouterLink>
    </div>
  </main>
</template>

<style scoped>

main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

a {
  color: #48F;
  text-decoration: none;
  padding-right: 8px;
  border-right: solid #888 1px;
  margin-right: 8px;
}

a:last-of-type {
  padding-right: 0px;
  border-right: solid #888 0px;
  margin-right: 0px;
}

h1 {
  font-weight: normal;
  font-size: 48px;
}

h1 span {
  font-weight: bold;
  font-size: 2em;
  color: #0000;
  background: linear-gradient(-15deg, #48F, #8F4);
  -webkit-background-clip: text;
  background-clip: text;
}

</style>