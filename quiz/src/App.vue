<template>
  <!--h1>{{ test }}</h1-->
  <div id="app">
    <Header class="app__header" 
      :score="answerScore"
      :total="answerTotal"
      v-if="questions.length"
      :activeQuestion="questions[questionIndex]"
    />
    <QuestionBox
      class="app__qbox"
      :addToScore="addScore"
      :addToTotal="addTotal"
      v-if="questions.length"
      :activeQuestion="questions[questionIndex]"
      :next="nextQuestion"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionBox from "./components/QuestionBox.vue";

export default {

  name: "App",
  components: {
    Header,
    QuestionBox,
  },

  data() {
    return {
      questions: [],
      questionIndex: 0,
      answerScore: 0,
      answerTotal: 0,
    };
  },

  computed: {
    test() {
      return this.$store.state.test
    }
  },

  methods: {
    nextQuestion() {
      this.questionIndex++;
    },
    addScore() {
      this.answerScore++;
      console.log(this.answerScore)
    },
    addTotal(){
      this.answerTotal++;
    }
  },

  mounted: function () {
    fetch(
      "https://opentdb.com/api.php?amount=10&type=multiple",
      { method: "get" }
    )
      .then((response) => {
        return response.json();
      })
      .then((jsonResult) => {
        this.questions = jsonResult.results;
      });
  },
};
</script>

<style>
  @import "assets/style/App.css";
</style>
