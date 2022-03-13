<template>
  <div class="chat-options" :class="{'visible': visible}">
    <span v-for="(option, i) in options" :key="i" @click="selectOption(i)">
      {{option.title}}
    </span>
    <div class="chat-options-input" v-if="!options" >
      <input type="text" ref="input" placeholder="Write your answer here"> 
      <span @click="submitText()"><img :src="require('/src/assets/img/go.png')"></span>
    </div>
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
    },
    submitText(){
      const name = this.$refs.input.value.trim() || 'Mr. Nobody'
      this.$emit('submittext', name)
    }
  }
}
</script>

<style lang="scss">
  @import '../assets/scss/main.scss';
  .chat-options {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding-top: 12px;
    margin-top: 24px;
    align-items: flex-start;
    max-height: 25%;
    flex-basis: auto;
    flex-shrink: 0;
    overflow: hidden;
    span {
      padding: 6px 12px;
      border-radius: 4px;
      margin: 4px;
      cursor: pointer;
      background: $light-yellow;
      color: #191426;
      font-weight: bold;
      font-size: 14px;
      &:hover {
        @media (min-width: $medium-device-breakpoint) { 
          background: $light-yellow-hover;
        }
      }
    }
    span, &-input { opacity: 0; }
    &-input {
      display: flex;
      flex-basis: 100%;
      padding: 0 30px;
      input {
        flex-basis: 100%;
        border: 0;
        background: rgba($purple-dark, .75);
        padding: 12px 16px;
        border-radius: 4px;
        color: $light-yellow;
        font-family: $main-font;
        font-size: 16px;
        &:focus-visible {
          outline: $purple-dark auto 0px;
        }
      }
      span {
        flex-basis: 10%;
        flex-shrink: 0;
        margin-left: 16px;
        display: flex;
        align-items: center;
        justify-content: center;
        img {
          height: 20px;
          width: auto;
        }
      }
    }
    &.visible {
      overflow-y: auto;
      span, .chat-options-input {
        opacity: 1;
        transition: opacity 1s linear 1.25s;
      }
    }
    
  }  
</style>