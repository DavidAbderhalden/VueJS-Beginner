<template>
  <div id="app">
    <Header class="app__header" />
    <QuestionBox
      class="app__qbox"
      v-if="questions.length"
      :activeQuestion="questions[i]"
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
      i: 0,
    };
  },

  methods: {
    nextQuestion() {
      this.i++;
    },
  },

  mounted: function () {
    fetch(
      "https://opentdb.com/api.php?amount=10&difficulty=medium&type=multiple",
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
#app {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
