<template class="qbox">
  <div class="qbox__wrapper">
    <h2 class="qbox__wrapper__title">QuestionBox</h2>
    <table class="qbox__wrapper__table">
      <tr>
        <th class="qbox__wrapper__table__question">Question</th>
      </tr>
      <tr>
        <td class="qbox__wrapper__table__answer">Answer 1</td>
      </tr>
      <tr>
        <td class="qbox__wrapper__table__answer">Answer 2</td>
      </tr>
      <tr>
        <td class="qbox__wrapper__table__answer">Answer 3</td>
      </tr>
      <tr>
        <td class="qbox__wrapper__table__answer">Answer 4</td>
      </tr>
    </table>

    <div class="qbox__wrapper__footer">
      <button class="qbox__wrapper__footer__button">Submit</button>
      <button class="qbox__wrapper__footer__button">Next</button>
    </div>
  </div>
</template>


<style>
.qbox__wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 50%;
  margin-top: 35px;
  background-color: rgb(238, 238, 238);
  padding-bottom: 50px;
}


.qbox__wrapper__table {
  width: 50%;
  border-spacing: 20px;
  margin-bottom: 20px;
}

.qbox__wrapper__table__question {
  padding: 10px;
  font-size: 20px;
  border-bottom: 1px solid black;
}

.qbox__wrapper__table__answer {
  padding: 8px;
}


.qbox__wrapper__footer{
    display: flex;
    justify-content: space-between;
    width: 25%;
}

.qbox__wrapper__footer__button{
    height: 30px;
    width: 90px;
    background-color: rgba(255, 181, 112, 0.986);
    border: 1px solid rgb(190, 190, 190);
}

.qbox__wrapper__footer__button:hover{
    background-color: rgba(255, 157, 65, 0.986);
}
</style>