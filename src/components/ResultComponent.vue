<template>
  <section class="result">
  <p class="result-text">{{ name }}, you belong to </p>
  <div class="result-illustration" :class="{'show': showHouse}" v-if="house">
    <img class="result-illustration-img" :src="require(`/src/assets/img/${result[house]?.shield}`)">
    <span class="result-illustration-glow" :style="{'background-color': result[house]?.color }"></span>
  </div>
  </section>
</template>

<script>

  export default {
    name: "ResultComponent",
    components: { },
    data(){
      return {
        showHouse: false,
        result: {
          g: {shield:'gryffindor.png', color: '#e55f73'},
          h: {shield:'hufflepuff.png', color: '#efc05d'},
          s: {shield:'slytherin.png', color: '#42a489'},
          r: {shield:'ravenclaw.png', color: '#79a9e6'}
        }
      }
    },
    props: {
      data: Object
    },
    computed: {
      house(){
        return this.data.house
      },
      name(){
        return this.data.name
      }
    },
    watch: {
      house: {
        immediate: true,
        handler() {
          setTimeout(() => this.showHouse = true, 1000)
        }
      }
    }
  }

</script>

<style lang="scss">
  @import '../assets/scss/main.scss';

  @keyframes glow {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.4); }
  }
  .result {
    display: flex;
    flex-basis: 100%;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    z-index: 1;
    position: relative;
    @media (min-width: $medium-device-breakpoint) {
      flex-basis: 40%;
    }
    &-text {
      font-size: 22px;
    }
    &-illustration {
      position: relative;
      width: 100%;
      height: 300px;
      transition: opacity .5s;
      opacity: 0;
      text-align: center;
      &.show {
        opacity: 1;
      }
      &-img {
        height: 100%;
        width: auto;
      }
      &-glow {
        height: 200px;
        width: 200px;
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
