<template>
  <Title :small="start && !finish">Sorting Hat</Title>
  
  <Intro  v-if="!start"  @start="startChat" />
  <Chat   v-if="start && !finish" @finish="setResults" />
  <Result v-if="finish" :data="result" />
  
  <div class="candles" :class="{show: start}">
    <Candle v-for="(p, i) in candlePositions"  :key="i" :top="p.top" :left="p.left" :right="p.right" />
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
        result: undefined,
        candlePositions: [
          //left
          {top: 'calc(50% - 250px)', left: 'calc(50% - 400px)'},
          {top: 'calc(50% - 180px)', left: 'calc(50% - 350px)'},
          {top: 'calc(50% - 170px)', left: 'calc(50% - 450px)'},
          {top: 'calc(50% - 100px)', left: 'calc(50% - 550px)'},
          {top: '50%',               left: 'calc(50% - 300px)'},
          {top: 'calc(50% - 55px)',  left: 'calc(50% - 350px)'},
          {top: 'calc(50% - 20px)',  left: 'calc(50% - 450px)'},
          //right
          {top: 'calc(50% - 250px)', right: 'calc(50% - 400px)'},
          {top: 'calc(50% - 180px)', right: 'calc(50% - 350px)'},
          {top: 'calc(50% - 170px)', right: 'calc(50% - 450px)'},
          {top: 'calc(50% - 100px)', right: 'calc(50% - 550px)'},
          {top: '50%',               right: 'calc(50% - 300px)'},
          {top: 'calc(50% - 55px)',  right: 'calc(50% - 350px)'},
          {top: 'calc(50% - 20px)',  right: 'calc(50% - 450px)'}

        ]
      }
    },
    methods: {
      startChat() {
        this.start = true
      },
      setResults(result) {
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
      height: 100%;
      width: 100%;
      overflow: hidden;
      position: absolute;
      pointer-events: none;
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
