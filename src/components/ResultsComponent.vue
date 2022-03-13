<template>
  <section id="result" class="result">
  <p class="result-text"> You belong to </p>
  <div class="result-illustration" :class="{'show': house}">
    <img class="result-illustration-img" :src="require(`/src/assets/img/${result[house]?.shield}`)">
    <span class="result-illustration-glow" :style="{'background-color': result[house]?.color }"></span>
  </div>
  </section>
</template>

<script>

  export default {
    name: "ResultsComponent",
    components: { },
    data(){
      return {
        result: {
          g: {shield:'gryffindor.png', color: '#e55f73'},
          h: {shield:'hufflepuff.png', color: '#efc05d'},
          s: {shield:'slytherin.png', color: '#42a489'},
          r: {shield:'ravenclaw.png', color: '#79a9e6'}
        }
      }
    },
    props: {
      house: String
    }
  
  }

</script>

<style lang="scss">
  @keyframes glow {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.4); }
  }
  .result {
    height: 100%;
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    z-index: 1;
    position: relative;
    &-text {
      color: white;
      font-size: 22px;
      font-style: italic;
    }
    &-illustration {
      position: relative;
      width: 100%;
      height: 300px;
      transition: opacity .5s;
      opacity: 0;
      &.show {
        opacity: 1;
      }
      &-img {
        height: 100%;
        width: auto;
      }
      &-glow{
        height: 200px;
        width: 200px;
        background: #ffcc66;
        border-radius: 50%;
        filter: blur(50px);
        z-index: -1;
        animation: glow 5s infinite linear;
        right: 10%;
        bottom: 10%;
        position: absolute;
      }
    }
  }

</style>
