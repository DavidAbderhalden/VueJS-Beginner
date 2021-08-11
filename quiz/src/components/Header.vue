<template class="header">
  <nav class="header__nav">
    <h2 class="header__nav__title">Quiz</h2>
    <p
      class="header__nav__difficulty"
      :class="{
        'header__nav__difficulty--easy': activeQuestion.difficulty == 'easy',
        'header__nav__difficulty--medium':activeQuestion.difficulty == 'medium',
        'header__nav__difficulty--hard': activeQuestion.difficulty == 'hard',
      }"
    >
      {{ activeQuestion.difficulty }}
    </p>
    <p class="header__nav__score">Correct: {{ score }}/{{ total }}</p>
  </nav>
</template>

<script>
export default {
  props: {
    score: Number,
    total: Number,
    activeQuestion: Object,
  },
};
</script>

<style>
  @import "../assets/style/Header.css";
</style>