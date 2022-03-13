<template>
  <Title :small="start">Sorting Hat</Title>
  
  <Intro  v-if="!start"  @start="startChat" />
  <Chat   v-if="start && !finish"  @finish="finishChat" />
  <Result v-if="finish" :data="result" />
  
  <div class="candles" :class="{show: start}">
    <!-- left candles -->
    <Candle top="15%" left="10%" />
    <Candle top="25%" left="5%" />
    <Candle top="40%" left="15%" />
    <Candle top="50%" left="20%" />
    <Candle top="45%" left="5%" />
    <Candle top="22%" left="15%" />


    <!-- right candles -->
    <Candle top="15%" right="20%" />
    <Candle top="25%" right="15%" />
    <Candle top="35%" right="20%" />
    <Candle top="50%" right="15%" />
    <Candle top="10%" right="5%" />
    <Candle top="34%" right="10%" />
  </div>
</template>

<script>

  import IntroComponent from './components/IntroComponent.vue'
  import ChatComponent from './components/ChatComponent.vue'
  import ResultComponent from './components/ResultComponent.vue'
  import CandleComponent from './components/CandleComponent.vue'
  import TitleComponent from './components/TitleComponent.vue'

  export default {
    name: "App",
    components: { 
      Intro: IntroComponent,
      Chat: ChatComponent,
      Result: ResultComponent,
      Candle: CandleComponent,
      Title: TitleComponent
    },
    data() {
      return {
        start: false,
        finish: false,
        result: undefined
      }
    },
    methods: {
      startChat() {
        this.start = true
      },
      finishChat(result) {
        this.result = result
        this.finish = true
      }
    }
  };
</script>

<style lang="scss">
  @import 'assets/scss/main.scss';
  $gradient: radial-gradient(circle, $purple-gradient-1 0%, $purple-gradient-2 35%, black 100%);
  /*style reset*/
  html, body {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    vertical-align: baseline;
    height: 100%;
    overflow: hidden;
  }
  * { 
    box-sizing: border-box;
  }  
  #app {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    background: $purple-gradient-1;
    background:  $gradient;
    background-image: url('/src/assets/img/bg.png'), $gradient;
    background-size: cover;
    font-family: $main-font;
    padding-top: 16px;
    color: $white;
    @media (min-width: 768px) { 
      padding-top: 40px;
    }
    .candles {
      opacity: 0;
      @media (max-width: $medium-device-breakpoint) { 
        display: none;
      }
    }
    div.show {
      transition: opacity .5s ease-in-out .5s;
      opacity: 1;
    }
  
  }
</style>
