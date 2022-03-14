<template>
  <section class="intro">
    <p class="intro-text">    
      — Slip me snug around your ears,<br>
      I've never yet been wrong,<br>
      I'll have alook inside your mind<br>
      And tell where you belong!<br>
    </p>
    <div class="intro-illustration">
      <img class="intro-illustration-img" :src="require('/src/assets/img/sorting-hat.png')">
      <span class="intro-illustration-glow"></span>
    </div>
    <span class="intro-button" @click="start()">Start</span>
  </section>
</template>

<script>

  export default {
    name: "IntroComponent",
    methods: {
      start(){
        this.$emit('start')
      }
    }
  };
</script>

<style lang="scss">
  @import '../assets/scss/main.scss';

  @keyframes fadeout {
    from { opacity: 1; max-height: 400px; }
    50%  { opacity: 0 }
    to   { opacity: 0; max-height: 0;}
  }
  $grey: #d1d6f1;
  
  .intro {
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: start;
    flex-basis: 70%;
    @media (min-width: $medium-device-breakpoint) {
      position: relative;
      flex-basis: 0;
    }
    &-text {
      font-size: 18px;
      line-height: 1.8;
      margin: 40px auto 32px;
      @media (min-width: $medium-device-breakpoint) { 
        font-size: 22px;
      }

    }
    &-button {
      min-width: 150px;
      position: relative;
      z-index: 1;
      text-transform: uppercase;
      font-weight: bold;
      padding: 12px;
      border-radius: 4px;
      margin: 4px;
      cursor: pointer;
      background: $light-yellow;
      color: #191426;
      transition: background .1s;
      &:hover {
        @media (min-width: $medium-device-breakpoint) { 
          background: $light-yellow-hover;
        }
      }
    }
    &-illustration {
      position: absolute;
      z-index: 1;
      right: 0;
      bottom: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      overflow: hidden;
      @media (min-width: $medium-device-breakpoint) { 
        overflow: visible;
      }
      &-img {
        position: absolute;
        border: 0;
        width: 400px;
        right: -120px;
        bottom: -60px;
        @media (min-width: $medium-device-breakpoint) { 
          width: 550px;
          bottom: -90px;
          right: -390px;
        }
      }
    }
  }

</style>
