<script setup>

    import { ref, computed } from 'vue'

    const questions = [
        {
            image: `${import.meta.env.BASE_URL}/question-images/earth-from-artemis-ii-day-2.jpeg`,
            question: "What is the name of the crew member that took this photograph?",
            answers: [
                {text: "Victor Glover", correct: false},
                {text: "Reid Wiseman", correct: true},
                {text: "Jeremy Hansen", correct: false},
                {text: "Christina Koch", correct: false}
            ]
        },
        {
            image: `${import.meta.env.BASE_URL}/question-images/earthset-artemis-ii.jpg`,
            question: "This photo was taken at 6:41 pm EDT on what day?",
            answers: [
                {text: "April 7, 2026", correct: false},
                {text: "April 8, 2026", correct: false},
                {text: "April 6, 2026", correct: true}
            ]
        },
        {
            image: `${import.meta.env.BASE_URL}/question-images/moon-and-earth-from-orion.jpg`,
            question: "The crew of the Artemis II traveled around the far side of the moon, beating the previous record for humans going the farthest from Earth. What was the name of the mission that held the record prior to Artemis II?",
            answers: [
                {text: "Apollo 13", correct: true},
                {text: "Apollo 17", correct: false},
                {text: "Apollo 11", correct: false}
            ]
        },
        {
            image: `${import.meta.env.BASE_URL}/question-images/orion-moon-earth-artemis-ii.jpg`,
            question: "This photograph was taken by one of the cameras on the solar arrays of which spacecraft?",
            answers: [
                {text: "The Integrity", correct: false},
                {text: "The Artemis II", correct: false},
                {text: "The Orion", correct: true}
            ]
        },
        {
            image: `${import.meta.env.BASE_URL}/question-images/christina-koch-views-earth.jpg`,
            question: "What is the name of the crew member who is looking back at the Earth in the image?",
            answers: [
                {text: "Victor Glover", correct: false},
                {text: "Reid Wiseman", correct: false},
                {text: "Jeremy Hansen", correct: false},
                {text: "Christina Koch", correct: true}  
            ]
        }, 
        {
            image: `${import.meta.env.BASE_URL}/question-images/solar-eclipse-from-artemis-ii.jpg`,
            question: "True or False: This image of a total solar eclipse was taken on the same day as the image of the Earthset from Question 1.",
            answers: [
                {text: "True", correct: true},
                {text: "False", correct: false}
            ]
        }
    ]

    const quizStarted = ref(false)
    const quizFinished = ref(false)

    const currentIndex = ref(0)
    const score = ref(0)

    const currentQuestion = computed(() => {
        return questions[currentIndex.value]
    })

    function startQuiz() {
        quizStarted.value = true
    }

    function nextQuestion(answer) {
        if (answer.correct) {
            score.value ++
        }

        const isLastQuestion = currentIndex.value === questions.length - 1

        if (isLastQuestion) {
            quizFinished.value = true
            return
        } else {
            currentIndex.value ++
        }
    }

    function restartQuiz() {
        currentIndex.value = 0
        score.value = 0
        quizFinished.value = false
        quizStarted.value = false
    }


</script>


<template>

    <main class="container mt-5">

        <!-- start screen-->
        <div v-if="!quizStarted" class="border border-light border-2 rounded custom-bg p-3 text-center m-5">
            <h3 class="my-3">Artemis II Quiz</h3>
            <p class="my-3">This quiz will test your Artemis II knowledge...and more specifically, how much you paid attention to the previous Bootstrap slideshow.</p>
            <button class="btn btn-light my-3" v-on:click="startQuiz">Click to Begin!</button>
        </div>

        <!--questions screen-->
        <div v-else-if="!quizFinished && quizStarted" class="border border-light border-2 rounded custom-bg p-3 text-center m-5">
            <h3 class="mb-3">Question #{{ currentIndex + 1 }}</h3>
            <img class="img-fluid rounded border border-light border-1" :src="currentQuestion.image" alt="" />
            <h4 class="mt-3">{{ currentQuestion.question }}</h4>
            <div class="d-flex flex-column gap-2">
                <button v-on:click="nextQuestion(answer)" v-for="answer in currentQuestion.answers" :key="answer.text" class="btn btn-light">{{ answer.text }}</button>
            </div>
        </div>

        <!--finish screen-->
        <div v-else class="border border-light border-2 rounded custom-bg p-3 text-center m-5">
            <h3 class="mb-3">Quiz Completed!</h3>
            <h4 class="mb-3">You scored {{ score }} / {{ questions.length }}</h4>
            <button class="btn btn-light" v-on:click="restartQuiz">Click to Reset the Quiz</button>
        </div>
    </main>

</template>


<style scoped>
:root {
    --card-bg-color: rgba(0, 0, 0, 0.5);
}

.custom-bg {
    background-color: var(--card-bg-color) !important;
    backdrop-filter: blur(6px);
    color: white;
}
</style>