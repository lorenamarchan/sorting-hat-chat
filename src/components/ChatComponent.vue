<template>
  <section id="chat" class="chat">
    <div class="chat-box" ref="chatbox">
      <ChatQuestionComponent v-for="(question, i) in questions" :key="i" :question="question" />
    </div>
    <ChatOptionsComponent :options="options" :visible="chatOptionsVisible" @select="selectOption"/>
    <ChatNavComponent @goBack="goBack" @redo="init"/>
  </section>
</template>

<script>
import chatFlow from '/src/assets/data/ChatFlow.json'
import ChatNavComponent from './ChatNavComponent.vue'
import ChatQuestionComponent from './ChatQuestionComponent.vue'
import ChatOptionsComponent from './ChatOptionsComponent.vue'

  
export default {
  name: "ChatComponent",
  components: {
    ChatNavComponent,
    ChatQuestionComponent,
    ChatOptionsComponent
  },
  data() {
    return {
      nQuestion: 0,
      questions: [],
      options: [],
      score: {g: 0, r: 0, h: 0, s: 0},
      chatOptionsVisible: false
    }
  },
  watch: {
    nQuestion:{
      immediate: true,
      handler(val) {
        this.addQuestion(chatFlow[val].title)
        this.setOptions(chatFlow[val].answers)
      }
    }
  },
  methods: {
    
    //questions
    
    addQuestion(text){
      this._add({text, type: 'sort-hat', img: 'sorting-hat.png'})
    },
    addAnswer(text){
      this._add({text, img: 'magic-wand.png'})
    },
    _add(obj){
      this.questions.push({id: this.nQuestion, ...obj})
      setTimeout(()=>this.scrollDown(this.$refs.chatbox))
    },
    scrollDown(element){
      element.scroll({
        top: element.scrollHeight,
        behavior: 'smooth'
      });
    },
    
    //navigation
    
    goBack(){
      this.questions = this.questions.filter(({id}) => id < this.nQuestion - 1 )
      this.nQuestion--
    },
    init(){
      this.questions = []
      this.nQuestion = 0
    },
    
    //options
    
    setOptions(options){
      this.options = options
      this.chatOptionsVisible = true
    },
    selectOption(index){
      if(this.chatOptionsVisible) {
        this.chatOptionsVisible = false
        //adds new score
        const answerScores = this.options[index].scores        
        Object.keys(this.score).map(house => this.score[house] += answerScores[house])  
        
        if(this.nQuestion < chatFlow.length - 1 ) {  //next questiob
          this.addAnswer(this.options[index].title)
          setTimeout(() => this.nQuestion++ , 1000) //delay for smoothness
        } else { //finish
          this.$emit('finish', this.getResults())
        }
      }
    },
    
    //result handling
    
    getResults(){
      const sortedScore = Object.keys(this.score)
        .sort((house1, house2) => {
          return this.score[house2] - this.score[house1]
        })
      return sortedScore[0]
    }
  }
}
</script>

<style lang="scss">
  .chat {
    height: calc(100% - 80px);
    width: 100%;
    max-width: 500px;
    padding: 16px;
    position: relative;
    display: flex;
    flex-direction: column;
    color: white;
    &-box {
      display: flex;
      align-items: flex-end;
      height: calc(100% - 170px);
      overflow-y: auto;
      flex-flow: column nowrap;
      flex-basis: 100%;
      position: relative;
      z-index: 2;
    }
  }
 
</style>
