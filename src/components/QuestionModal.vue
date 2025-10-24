<template>
    <div class="fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center z-50">
        <div class="bg-white p-6 rounded max-w-2xl w-full text-gray-900 overflow-y-auto max-h-[90vh] shadow-2xl relative">
            <h2 class="text-2xl font-bold mb-4 mt-0">Вопрос</h2>
            <QuestionViewer :question="question" :show-answer="questionAnswered" />

            <div class="mt-6" v-if="players.length">
                <h3 class="text-lg font-semibold mb-2">Кто отвечает?</h3>
                <div class="grid grid-cols-2 gap-4">
                    <button
                        v-for="player in players"
                        :key="player.name"
                        class="px-4 py-2 bg-gray-100 hover:bg-gray-200 rounded border border-gray-300"
                        @click="$emit('answer', player, question.price)"
                        :disabled="answeredPlayers.includes(player.name) || questionAnswered"
                    >
                        {{ player.name }}
                    </button>
                </div>
                <button
                    class="mt-4 text-sm text-gray-500 hover:underline"
                    @click="$emit('no-answer')"
                    :disabled="questionAnswered"
                >
                    Завершить вопрос (никто не ответил)
                </button>
            </div>

            <div class="mt-6 flex justify-end">
                <button
                    class="px-4 py-2 bg-emerald-600 text-white rounded hover:bg-emerald-500"
                    @click="$emit('close')"
                    :disabled="!questionAnswered"
                >
                    Закрыть
                </button>
            </div>

            <template v-if="showDecorNewYear">
                <img
                    src="../assets/newYear/top-right.webp"
                    alt="picture new year"
                    class="absolute top-0 right-0 w-30 pointer-events-none"
                >

                <img
                    src="../assets/newYear/top-left.webp"
                    alt="picture new year"
                    class="absolute bottom-0 -left-0.2 w-25 pointer-events-none -rotate-90"
                >
            </template>
        </div>
    </div>
</template>

<script setup>
import QuestionViewer from './QuestionViewer.vue'

defineProps({
    question: Object,
    players: Array,
    answeredPlayers: Array,
    questionAnswered: Boolean,
    showDecorNewYear: Boolean
});

defineEmits(['answer', 'close', 'no-answer']);
</script>
