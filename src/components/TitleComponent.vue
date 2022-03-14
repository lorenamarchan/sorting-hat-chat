<template>    
  <div class="title" :class="{'small': small}">
    <CandleComponent class="intro-candle" top="25px" left="calc(50% - 140px)" />
    <h1 class="title-text"><slot /></h1>
    <CandleComponent class="intro-candle" top="25px" right="calc(50% - 140px)" />
  </div>
</template>

<script>
  import CandleComponent from './CandleComponent.vue'

  export default {
    name: "TitleComponent",
    props: {
      small: Boolean
    },
    components: {
      CandleComponent
    }
  }
</script>

<style lang="scss">
  @import '../assets/scss/main.scss';

  .title {
    &-text {     
      font-family: $title-font;
      font-size: 80px;
      text-align: center;
      font-weight: 400;
      margin: 0;
      text-shadow: 6px 6px 8px $purple-shadow;
      letter-spacing: 2px;
      transition: all .5s;
      @media (min-width: $medium-device-breakpoint) { 
        font-size: 100px;
      }
    }
    .candle {
      opacity: 0;
      transition: opacity .5s linear .5s;
      @media (min-width: $medium-device-breakpoint) { 
        display: none;
      }
    }
    &.small {
      .title-text { font-size: 50px; }
      .candle { opacity: 1; }
    }
  }
</style>