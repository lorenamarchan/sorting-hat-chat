<template>
  <Title :small="started">Sorting Hat</Title>
  
  <Intro @start="startChat" ref="intro" v-show="!started"/>
  <Chat  v-show="started && !finished" @finish="finishChat" />
  <Results :house="result" v-if="finished"/>
  
  <div class="candles" v-show="started" key="candles">
    <!-- left candles -->
    <Candle top="15%" left="10%" />
    <Candle top="25%" left="5%" />
    <Candle top="40%" left="15%" />
    <Candle top="50%" left="25%" />
    <Candle top="65%" left="5%" />
    <Candle top="75%" left="15%" />


    <!-- right candles -->
    <Candle top="15%" right="20%" />
    <Candle top="25%" right="10%" />
    <Candle top="35%" right="25%" />
    <Candle top="50%" right="15%" />
    <Candle top="70%" right="10%" />
    <Candle top="80%" right="15%" />
  </div>

</template>

<script>

  import IntroComponent from './components/IntroComponent.vue'
  import ChatComponent from './components/ChatComponent.vue'
  import ResultsComponent from './components/ResultsComponent.vue'
  import CandleComponent from './components/CandleComponent.vue'
  import TitleComponent from './components/TitleComponent.vue'

  export default {
    name: "App",
    components: { 
      Intro: IntroComponent,
      Chat: ChatComponent,
      Results: ResultsComponent,
      Candle: CandleComponent,
      Title: TitleComponent
    },
    data() {
      return {
        started: false,
        finished: false,
        result: 'g'
      }
    },
    methods: {
      startChat() {
        this.started = true
      },
      finishChat(result) {
        this.result = result
        this.finished = true
      }
    }
  };
</script>

<style lang="scss">
  
  @font-face {
    font-family: magicSchool;
    src: url('/src/assets/fonts/magic-school.ttf');
  }
  @font-face {
    font-family: merriweather;
    src: url('/src/assets/fonts/Merriweather-Regular.ttf');
  }
  @font-face {
    font-family: merriweather;
    font-style: italic;
    src: url('/src/assets/fonts/Merriweather-Italic.ttf');
  }
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
    height: 100%;
    background: #251d3b;
    background: radial-gradient(circle,#251d3b 0%, #201930 35%, #11111d 100%);
    font-family: merriweather;
    padding-top: 32px;
    .candles {
      @media (max-width: 650px) { 
          display: none;
      }
    }
  
  }
</style>
