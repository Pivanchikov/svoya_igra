// App.vue
<template>
    <div class="p-6 min-h-screen bg-gradient-to-b from-sky-100 to-blue-200 text-gray-900">
        <div class="text-center mb-6">
            <h1 class="text-5xl font-extrabold mb-4">Своя Игра — Тур {{ currentRound + 1 }}</h1>
        </div>

        <AddPlayers v-if="!gameStarted" :players="players" v-model:new-player="newPlayer" @add-player="addPlayer" @start="startGame" />

        <template v-else>
            <PlayerList :players="players" @reset="showResetConfirm = true" />
            <RoundSelector :rounds="rounds" :current-round="currentRound" @switch="switchRound" />
            <QuestionBoard :themes="rounds[currentRound].themes" @open-question="openQuestion" />
        </template>

        <QuestionModal
            v-if="activeQuestion"
            :question="activeQuestion"
            :players="players"
            :answered-players="answeredPlayers"
            :question-answered="questionAnswered"
            @answer="handleAnswer"
            @no-answer="noAnswer"
            @close="closeQuestion"
        />

        <ResetModal v-if="showResetConfirm" @confirm="resetGame" @cancel="showResetConfirm = false" />
    </div>
</template>

<script setup>
import { reactive, ref } from 'vue'
import questionData from './questions.json'
import AddPlayers from './components/AddPlayers.vue'
import PlayerList from './components/PlayerList.vue'
import RoundSelector from './components/RoundSelector.vue'
import QuestionBoard from './components/QuestionBoard.vue'
import QuestionModal from './components/QuestionModal.vue'
import ResetModal from './components/ResetModal.vue'

const rounds = reactive(loadData('rounds', questionData.rounds))
const currentRound = ref(loadData('currentRound', 0))
const activeQuestion = ref(null)
const players = ref(loadData('players', []))
const newPlayer = ref('')
const answeredPlayers = ref([])
const showResetConfirm = ref(false)
const gameStarted = ref(loadData('gameStarted', false))
const questionAnswered = ref(false)

function addPlayer(name) {
    const trimmed = name.trim()
    if (trimmed && !players.value.find(p => p.name.toLowerCase() === trimmed.toLowerCase())) {
        players.value.push({ name: trimmed, score: 0 })
        saveAll()
    }
}

function startGame() {
    gameStarted.value = true
    saveAll()
}

function switchRound(index) {
    currentRound.value = index
    saveAll()
}

function openQuestion(themeIndex, qIndex) {
    const q = rounds[currentRound.value].themes[themeIndex].questions[qIndex]
    if (q.asked) return
    activeQuestion.value = q
    q.asked = true
    questionAnswered.value = false
    answeredPlayers.value = []
    saveAll()
}

function closeQuestion() {
    activeQuestion.value = null
    answeredPlayers.value = []
    questionAnswered.value = false
    saveAll()
}

function handleAnswer(player, price) {
    const correct = confirm(`Игрок ${player.name} дал правильный ответ?`)
    player.score += correct ? price : -price
    answeredPlayers.value.push(player.name)
    if (correct) questionAnswered.value = true
    saveAll()
}

function resetGame() {
    localStorage.clear()
    location.reload()
}

function saveAll() {
    localStorage.setItem('rounds', JSON.stringify(rounds))
    localStorage.setItem('players', JSON.stringify(players.value))
    localStorage.setItem('currentRound', currentRound.value)
    localStorage.setItem('gameStarted', JSON.stringify(gameStarted.value))
}

function noAnswer() {
    questionAnswered.value = true
    saveAll()
}

function loadData(key, fallback) {
    try {
        const stored = localStorage.getItem(key)
        return stored ? JSON.parse(stored) : fallback
    } catch (e) {
        return fallback
    }
}
</script>

<style scoped>
.line-through {
    text-decoration: line-through;
}
</style>
