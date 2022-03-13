<template>
  <div class="chat-options" :class="{'visible': visible}">
    <span v-for="(option, i) in options" :key="i" @click="selectOption(i)">
      {{option.title}}
    </span>
  </div>
</template>

<script>
export default {
  name: "ChatOptionsComponent",
  props: {
    visible: Boolean,
    options: Array
  },
  methods: {
    selectOption(i){
      this.$emit('select', i)
    }
  }
}
</script>

<style lang="scss">
  .chat-options {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding-top: 12px;
    margin-top: 24px;
    overflow-y: auto;
    align-items: flex-start;
    max-height: 25%;
    flex-basis: auto;
    flex-shrink: 0;
    span {
      border: solid 1px;
      padding: 6px 12px;
      border-radius: 4px;
      margin: 4px;
      opacity: 0;
      cursor: pointer;
    }
    &.visible {
      span {
        opacity: 1
      }
    }
  }  
</style>