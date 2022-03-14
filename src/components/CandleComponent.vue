<template>
    <div class="candle" :style="{'animation-delay': randomDelay(), top, left, right, bottom }">
      <img :src="require('/src/assets/img/candle.png')">
      <span class="glow" :style="{'animation-delay': randomDelay() }"></span>
    </div>
</template>

<script>
export default {
  name: "CandleComponent",
  props: {
    top: String,
    left: String,
    right: String,
    bottom: String
  },
  methods: {
    randomDelay(){
      return (Math.random()*6).toFixed(2) + 's'
    }
  }
}
</script>

<style lang="scss">
  @import '../assets/scss/main.scss';

  @keyframes glow {
    from, to { transform: scale(.9); }
    50% { transform: scale(1.2); }
  }
  @keyframes floating {
    from { transform: translate(0,  0px); }
    65%  { transform: translate(0, 15px); }
    to   { transform: translate(0, -0px); }    
  }
  .candle {
    position: absolute;
    z-index: 1;
    animation: floating 6s infinite;
    img {
      height: 40px;
    }
    .glow {
      position: absolute;
      height: 30px;
      width: 30px;
      top: -10px;
      background: rgba($orange, 20%);
      left: -10px;
      border-radius: 50%;
      z-index: -1;
      animation: glow 4s infinite;
    }
  }
</style>