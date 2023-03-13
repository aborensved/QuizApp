<script setup>
import Question from "../components/Question.vue";
import QuizHeader from "../components/QuizHeader.vue";
import Result from "../components/Result.vue"; 
import { useRoute, RouterLink } from "vue-router"
import { ref, watch, computed } from "vue";
import quizes from "../data/quizes.json";

const route = useRoute();
const quizId = parseInt(route.params.id);
const quiz = quizes.find(q => q.id === quizId);
const currentQuestionIndex = ref(0);
const numberOfCorrectAnswers = ref(0);
const showResults = ref(false);

// const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)

// watch(() => currentQuestionIndex.value, () => {
//   questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
// })

const questionStatus = computed(() => `${currentQuestionIndex.value}/${quiz.questions.length}`);
const barPercentage = computed(() => `${currentQuestionIndex.value/quiz.questions.length * 100}%`)

const onOptionSelected = (isCorrect) => {
  if(isCorrect){
    numberOfCorrectAnswers.value++;
  }

  if(quiz.questions.length -1  === currentQuestionIndex.value){
    showResults.value = true;
  }

  currentQuestionIndex.value++;
}

</script>

<template>
  <div>
    <QuizHeader 
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />
    <div>
      <Question 
        v-if="!showResults"
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSelected"
      />
      <Result 
        v-else
        :quizQuestionLength="quiz.questions.length"
        :numberOfCorrectAnswers="numberOfCorrectAnswers"
        />
    </div>
    <RouterLink class="button-74" to="/">Home Page</RouterLink>
    
  </div>
</template>

<style>

/* CSS */
.button-74 {
  background-color: #fbeee0;
  border: 2px solid #422800;
  border-radius: 30px;
  box-shadow: #422800 4px 4px 0 0;
  color: #422800;
  cursor: pointer;
  display: inline-block;
  font-weight: 600;
  font-size: 18px;
  padding: 0 18px;
  line-height: 50px;
  text-align: center;
  text-decoration: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-74:hover {
  background-color: #fff;
}

.button-74:active {
  box-shadow: #422800 2px 2px 0 0;
  transform: translate(2px, 2px);
}

@media (min-width: 768px) {
  .button-74 {
    min-width: 120px;
    padding: 0 25px;
  }
}
</style>
