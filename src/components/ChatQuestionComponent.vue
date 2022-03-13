<template>
  <div class="chat-question" :class="question.type">
    <img class="chat-question-img"  :src="require(`/src/assets/img/${question.img}`)">
    <p class="chat-question-text"><span>{{ question.text }}</span></p>
  </div>
</template>

<script>
export default {
  name: "ChatQuestionComponent",
  props: {
    question: Object
  }
}
</script>

<style lang="scss">
  @keyframes scaleIn {
    from { transform: scale(0); }
    to { transform: scale(1); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  
  .chat-question {
    display: flex;
    align-items: flex-end;
    width: 100%;
    justify-content: flex-start;
    font-style: italic;
    &:first-child {
      margin-top: auto;
    }
    &-text {
      background: rgba(#120e1a, .35);
      padding: 12px 16px;
      border-radius: 4px;
      flex-basis: 80%;
      position: relative;
      margin: 8px 0;
      z-index: 1;
      /*color: #ba9278;*/
      color: #d4c5ab;
      transform-origin: bottom left;
      animation: scaleIn .4s ease-in-out .1s both;
      span {
        animation: fadeIn .3s ease-in-out .6s both;
      }
      &::after {
        content: "";
        position: absolute;
        bottom: 12px;
        left: -16px;
        border: solid 8px transparent;
        border-bottom-color: rgba(#120e1a, .35);
        border-right-color: rgba(#120e1a, .35);
        z-index: -1;
      }
    }
    &-img {
      width: 50px;
      border-radius: 50%;
      margin: 0 12px 0 0;
    }
    &.sort-hat {
      flex-direction: row-reverse;
      text-align: right;
      .chat-question {
        &-text {
          background: rgba(#120e1a, .5);
          transform-origin: bottom right;
          color: white;
          &::after {
            left: auto;
            right: -16px;
            border-bottom-color: rgba(#120e1a, .5);
            border-right-color: transparent;
            border-left-color: rgba(#120e1a, .5);
          }
        }
        &-img {
          margin: 0 0 0 12px;
        }
      }
    }
  }
</style>