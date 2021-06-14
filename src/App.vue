<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="less">
html {
  font-family: "Roboto", "Helvetica", sans-serif;
}

#app {
  max-width: 480px;
  overflow-y: hidden;
  margin: 0px auto;
  display: block;
  background: rgb(180,58,98);
  background: linear-gradient(32deg, rgba(180,58,98,1) 0%, rgba(252,69,69,1) 100%);
  border-radius: 0.5rem;
  -webkit-box-shadow: 0px 4px 8px 1px rgba(91, 91, 91, 0.3);
  box-shadow: 0px 4px 8px 1px rgba(91, 91, 91, 0.3);
  padding: 1rem;
  position: relative;
  height: 480px;
}
</style>
