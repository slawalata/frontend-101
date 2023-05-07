<script setup>
import {RouterLink} from "vue-router";

const {
    quizQuestionLength,
    numberOfCorrectAnswer
} =
    defineProps([
        "quizQuestionLength",
        "numberOfCorrectAnswer"
    ])

</script>

<template>
    <div class="result">
        <p>Your Result...</p>
        <h1>{{ numberOfCorrectAnswer }}/{{ quizQuestionLength }}</h1>
        <RouterLink to="/">GO Back</RouterLink>
    </div>
</template>

<style scoped>
.result {
    text-align: center;
    padding: 100px 0;
}

p {
    font-size: 25px
}

h1 {
    font-size: 80px;
}

</style>
