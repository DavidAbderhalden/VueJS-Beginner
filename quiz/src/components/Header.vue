<template class="header">
    <nav class="header__nav">
        <h2 class="header__nav__title" >Quiz</h2>
        <p class="header__nav__score" >Correct: {{ score }}/{{ total }}</p>
    </nav>
</template>

<script>
export default {
  props: {
    score: Number,
    total: Number
  },
}
</script>

<style>
.header__nav {
    width: 60%;
    display: flex;
    justify-content: center;
    align-items: center;
    border-bottom: 1px solid gray;

}
.header__nav__score{
    margin-left: 50%;
    padding: 0px;

}
</style>