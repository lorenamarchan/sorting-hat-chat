<template>
  <section id="chat" class="chat">
    <div class="chat-box" ref="chatbox">
      <ChatQuestionComponent v-for="(question, i) in questions" :key="i" :question="question" />
    </div>
    <ChatOptionsComponent :options="options" :visible="chatOptionsVisible" @select="selectOption" @submittext="submitText"/>
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
      userName: '',
      nQuestion: 0,
      questions: [],
      options: [],
      score: {g: 0, r: 0, h: 0, s: 0},
      chatOptionsVisible: false,
      history: []
    }
  },
  watch: {
    nQuestion:{
      immediate: true,
      handler(val) {
        setTimeout(() => {
          this.addQuestion(chatFlow[val].title)
          this.setOptions(chatFlow[val].answers)
          if(chatFlow[val].continue){
            this.nQuestion++
          }
        }, 1500) //delay for animation
  
      }
    }
  },
  methods: {
    
    //questions
    
    addQuestion(text){
      this._add('question', {text, type: 'sort-hat', img: 'sorting-hat.png'})
    },
    
    addAnswer(text){
      this._add('answer', {text, img: 'magic-wand.png'})
    },
    
    _add(type, obj){
      this.questions.push({id: this.nQuestion, ...obj})
      this.history.push({id: this.nQuestion, type})
      setTimeout(()=>this.scrollDown(this.$refs.chatbox))
      
    },
    
    scrollDown(element){
      element.scroll({
        top: element.scrollHeight,
        behavior: 'smooth'
      })
    },

    //options
    
    submitText(name){
      this.userName = name
      this.addAnswer(name)
      this.chatOptionsVisible = false
      this.nQuestion++
    },
    
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
        
        //go to next question
        if(this.nQuestion < chatFlow.length - 1 ) {
          this.addAnswer(this.options[index].title)
          this.nQuestion++
         //finish chat
        } else {
          this.$emit('finish', this.getResult())
        }
      }
    },
        
    //navigation
    
    goBack(){
      const lastAnswer = this.history.reverse().find( obj => obj.type === 'answer')
      this.questions = this.questions.filter(({id}) => id < lastAnswer.id)
      this.history = this.history.filter(({id}) => id <= lastAnswer.id)
      this.nQuestion = lastAnswer.id
    },
    
    init(){
      this.questions = []
      this.nQuestion = 0
    },
    
    //result handling
    
    getResult(){
      const sortedScore = Object.keys(this.score)
                                .sort((h1, h2) => this.score[h2] - this.score[h1])
      return {name: this.userName, house: sortedScore[0]}
    }
  }
}
</script>

<style lang="scss">
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
   @import '../assets/scss/main.scss';
  .chat {
    height: calc(100% - 80px);
    width: 100%;
    max-width: 500px;
    padding: 16px;
    position: relative;
    display: flex;
    flex-direction: column;
    max-height: 700px;
    animation: fadeIn 1s both 1s;
    &-box {
      display: flex;
      align-items: flex-end;
      overflow-y: auto;
      flex-flow: column nowrap;
      flex-basis: 100%;
      position: relative;
      z-index: 2;
    }
  }
 
</style>
