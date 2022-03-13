<template>
  <section class="intro">
    <p class="intro-text">    
      Slip me snug around your ears,<br>
      I've never yet been wrong,<br>
      I'll have alook inside your mind<br>
      And tell where you belong!<br>
    </p>
    <div class="intro-illustration">
      <img class="intro-illustration-img" :src="require('/src/assets/img/sorting-hat.png')">
      <span class="intro-illustration-glow"></span>
    </div>
    <button class="intro-button" @click="start()">Start</button>
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
    flex-basis: 100%;
    color: white;
    align-items: center;
    justify-content: center;
    &-text {
      font-size: 22px;
      line-height: 1.8;
      margin: 40px auto 32px;
      font-style: italic;

    }
    &-button {
      background: transparent;
      border: solid 1px $grey;
      color: white;
      padding: 12px;
      min-width: 150px;
      font-size: 16px;
      font-family: merriweather;
      cursor: pointer;
      position: relative;
      border-radius: 4px;
      z-index: 1;
      text-transform: uppercase;
      font-weight: bold;
    }
    &-illustration {
      position: absolute;
      z-index: 1;
      right: -90px;
      bottom: -70px;
      &-img, &-glow {
        position: absolute;
        border: 0;
        bottom: 0;
        right: 0;
        width: 750px;
      }
    }
  }

</style>
