<template class="qbox">
  <div class="qbox__wrapper">
    <h2 class="qbox__wrapper__title">Questions and Answers</h2>
    <table class="qbox__wrapper__table">
      <tr>
        <th class="qbox__wrapper__table__question">
          {{ activeQuestion.question }}
        </th>
      </tr>
      <tr
        v-for="(answer, index) in shuffledAnswers"
        :key="index"
        @click.prevent="selectIndex(index)"
        :class="[selectedIndex === index ? 'qbox__wrapper__table__answer--selected' : '']"
      >
        <td class="qbox__wrapper__table__answer">{{ answer }}</td>
      </tr>
    </table>

    <div class="qbox__wrapper__footer">
      <button class="qbox__wrapper__footer__button" @click="checkAnswer" :class="[submitted ? 'qbox__wrapper__footer__button--disabled' : '']">Submit</button>
      <button class="qbox__wrapper__footer__button" :disabled="!submitted" @click="getNextQuestion">Next</button>
    </div>
  </div>
</template>


<script>
import _ from 'lodash'
export default {
  props: {
    activeQuestion: Object,
    next: Function,
    add: Function,
    addTotal: Function
  },
  data() {
    return {
      shuffledAnswers: [],
      selectedIndex: null,
      correct: false,
      submitted: false,
    };
  },

  // Variables can be parsed to the watch function. It will react as soon as they update. 
  watch: {
    activeQuestion: {
      immediate: true,           // Immediate is also running the function on creation.
      handler(){
        this.resetSelected()
        this.shuffleAnswers()
      }
    }
  },

  methods: {
    resetSelected(){
      this.selectedIndex = null;
    },

    selectIndex(index) {
      this.selectedIndex = index;
    },

    shuffleAnswers() {
      let answers = [...this.activeQuestion.incorrect_answers, this.activeQuestion.correct_answer];
      this.shuffledAnswers = _.shuffle(answers)
    },
    checkAnswer() {
      if(!this.submitted) {
        this.addTotal()
        this.submitted = true
        let correctIndex = this.shuffledAnswers.indexOf(this.activeQuestion.correct_answer)
        if(this.selectedIndex == correctIndex) {
          this.correct = true
          this.add()
        }
      }
    },
    getNextQuestion() {
      this.submitted = false
      this.correct = false
      this.next()
    }
  },

  computed: {
    /*allAnswers() {
      let answers = [...this.activeQuestion.incorrect_answers];
      answers.push(this.activeQuestion.correct_answer);
      return answers;
    },*/
  },
}
</script>


<style>
.qbox {
  --background: rgb(224, 224, 224);
}

.qbox__wrapper {
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 50%;
  margin-top: 35px;
  background-color: rgb(238, 238, 238);
  padding-bottom: 50px;
}
.qbox__wrapper__title {
  margin-bottom: 0px;
  padding-bottom: 0px;
}

.qbox__wrapper__table {
  width: 70%;
  border-spacing: 15px;
  margin-bottom: 20px;
}

.qbox__wrapper__table__question {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  color: rgb(112, 112, 112);
  font-weight: normal;
  height: 70px;
  padding: 10px 10px 20px 10px;
  font-size: 20px;
  border-bottom: 1px solid rgb(160, 160, 160);
}

.qbox__wrapper__table__answer {
  padding: 15px;
  border: 1px solid var(--background);
}

.qbox__wrapper__table__answer:hover {
  outline: 1px solid rgb(163, 163, 163);
  background-color: rgba(0, 0, 0, 0.096);
  cursor: pointer;
}
.qbox__wrapper__table__answer--selected {
  outline: 1px solid rgb(163, 163, 163);
  background-color: rgba(255, 181, 112, 0.986);

}

.qbox__wrapper__footer {
  display: flex;
  justify-content: space-between;
  width: 35%;
}

.qbox__wrapper__footer__button {
  font-size: 16px;
  color: rgb(48, 48, 48);
  height: 40px;
  width: 120px;
  background-color: rgba(255, 181, 112, 0.986);
  border: 1px solid rgb(190, 190, 190);
  border-radius: 4px;
}

.qbox__wrapper__footer__button:hover {
  background-color: rgba(255, 157, 65, 0.986);
  border: 2px solid rgb(37, 37, 37);
  cursor: pointer;
}

.qbox__wrapper__footer__button--disabled {
  background-color: rgb(221, 221, 221);
}

.qbox__wrapper__footer__button--disabled:hover {
  background-color: rgb(221, 221, 221);
  border: 1px solid rgb(190, 190, 190);
  cursor: unset;
}

</style>