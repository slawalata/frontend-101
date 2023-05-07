<script setup>
import {useRoute} from "vue-router";
import Question from "../views/Question.vue";
import QuizHeader from "../components/QuizHeader.vue";
import quizes from "../data/quizes.json"
import {ref, computed} from "vue";
import Result from "../components/Result.vue";

const route = useRoute()
const quizId = parseInt(route.params.id)
const quiz = quizes.find(q => q.id === quizId)
const currentQuestionIndex = ref(0)
const numberOfCorrectAnswer = ref(0)
const showResults = ref(false)

// use `` not '' to join string and combining attribute as string.
const questionStatus = computed(
    () => `${currentQuestionIndex.value}/${quiz.questions.length}`
)

const barPercentage = computed(
    () => `${currentQuestionIndex.value / quiz.questions.length * 100}%`
)

const onOptionSelected = (isCorrect) => {
    if (isCorrect) {
        numberOfCorrectAnswer.value++;
    }

    if (quiz.questions.length - 1 === currentQuestionIndex.value) {
        showResults.value = true
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
                    :numberOfCorrectAnswer="numberOfCorrectAnswer"
            />

        </div>

        <!--        <button @click="currentQuestionIndex++">Click me</button>-->
    </div>
</template>

<style scoped>


</style>
