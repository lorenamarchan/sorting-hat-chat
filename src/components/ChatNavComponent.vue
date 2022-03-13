<template>
  <div class="chat-nav">
    <span @click="goBack()">
      <img :src="require('/src/assets/img/back.png')">
      Back
    </span>
    <span @click="redo()">
      <img :src="require('/src/assets/img/redo.png')">
      Start again
    </span>
  </div>
</template>

<script>
export default {
  name: "ChatNavComponent",
  methods: {
    goBack(){
      this.$emit('goBack')
    },
    redo(){
      this.$emit('redo')
    }
  }
}
</script>

<style lang="scss">
  @import '../assets/scss/main.scss';
  $size: 20px;
  .chat-nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 12px 20px 0;
    font-size: 12px;
    span {
      display: flex;
      flex-direction: column;
      align-items: center;
      cursor: pointer;
      color: $light-yellow;
      img {
        height: $size;
        width: $size;
        flex-shrink: 0;
        margin-bottom: 4px;
        transition: transform .2s;

      }
      &:hover {
        img {
          transform: scale(1.1)
        }
      }
    }
  }
</style>