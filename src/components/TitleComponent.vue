<template>    
  <div class="title" :class="{'small': small}">
    <CandleComponent class="intro-candle" top="10px" left="calc(50% - 140px)" />
    <h1 class="title-text"><slot /></h1>
    <CandleComponent class="intro-candle" top="10px" right="calc(50% - 140px)" />
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
  .title {
    transform: translateY(150px);
    &.small {
      transform: translateY(0);
      .title-text {
        font-size: 50px;
      }
      .candle {
        opacity: 1;
      }
    }
    &, &-text {
      transition: all 2s ease-out;
    }
    &-text {     
      font-family: magicSchool;
      font-size: 100px;
      text-align: center;
      font-weight: 400;
      margin: 0;
      text-shadow: 6px 6px 16px #100c1a;
      letter-spacing: 2px;
      color: white;
    }
    .candle {
      opacity: 0;
      transition: opacity .5s linear 2s;
      @media (min-width: 650px) { 
        display: none;
      }
    }
  }
</style>