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
      >
        <td 
        class="qbox__wrapper__table__answer"
        @click.prevent="selectIndex(index)"
        :class="{
          'qbox__wrapper__table__answer--locked': submitted,
          'qbox__wrapper__table__answer--correct': correctIndex === index && submitted,
          'qbox__wrapper__table__answer--wrong': selectedIndex === index && submitted && selectedIndex !== correctIndex,
          'qbox__wrapper__table__answer--selected': selectedIndex === index && !submitted,
        }"
        >{{ answer }}</td>
      </tr>
    </table>

    <div class="qbox__wrapper__footer">
      <button
        class="qbox__wrapper__footer__button"
        :disabled="submitted || selectedIndex === null"
        @click="checkAnswer"
        :class="[
          submitted || selectedIndex === null
            ? 'qbox__wrapper__footer__button--disabled'
            : '',
        ]"
      >
        Submit
      </button>
      <button
        class="qbox__wrapper__footer__button"
        :disabled="!submitted"
        @click="getNextQuestion"
        :class="[!submitted ? 'qbox__wrapper__footer__button--disabled' : '']"
      >
        Next
      </button>
    </div>
  </div>
</template>


<script>
import _ from "lodash";
export default {
  props: {
    activeQuestion: Object,
    next: Function,
    addToScore: Function,
    addToTotal: Function,
  },
  data() {
    return {
      shuffledAnswers: [],
      selectedIndex: null,
      correct: false,
      submitted: false,
      correctIndex: null,
    };
  },

  // Variables can be parsed to the watch function. It will react as soon as they update.
  watch: {
    activeQuestion: {
      immediate: true, // Immediate is also running the function on creation.
      handler() {
        this.submitted = false;
        this.correct = false;
        this.resetAll();
        this.shuffleAnswers();
      },
    },
  },

  methods: {
    resetAll() {
      this.selectedIndex = null;
    },

    selectIndex(index) {
      if (!this.submitted) {
        this.selectedIndex = index;
      }
    },

    shuffleAnswers() {
      let answers = [
        ...this.activeQuestion.incorrect_answers,
        this.activeQuestion.correct_answer,
      ];
      this.shuffledAnswers = _.shuffle(answers);
    },
    checkAnswer() {
      this.addToTotal();
      this.submitted = true;
      this.correctIndex = this.shuffledAnswers.indexOf(
        this.activeQuestion.correct_answer
      );
      if (this.selectedIndex == this.correctIndex) {
        this.correct = true;
        this.addToScore();
      }
    },
    getNextQuestion() {
      this.next();
    },
  },
};
</script>


<style>
@import "../assets/style/QuestionBox.css";
</style>