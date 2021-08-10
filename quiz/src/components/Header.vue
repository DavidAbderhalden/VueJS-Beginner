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
.header__nav {
  width: 60%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  border-bottom: 1px solid gray;
}
.header__nav__score {
  padding: 0px;
}

.header__nav__difficulty{
  font-size: 18px;
}

.header__nav__difficulty--easy{
  color: green;
} 

.header__nav__difficulty--medium{
  color: orange;
} 

.header__nav__difficulty--hard{
  color: red;
} 
</style>