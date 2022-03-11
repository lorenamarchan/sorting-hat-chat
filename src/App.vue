<template>
  <div>holi</div>
  <ChatSorter />
</template>

<script>

  import ChatSorter from './components/ChatSorter.vue'

  export default {
    name: "App",
    components: { ChatSorter }
  };
</script>

<style lang="scss">
  /*style reset*/
  html, body {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    vertical-align: baseline;
  }
  * { 
    box-sizing: border-box;
  }  
</style>
