<template>
    <div class="flex justify-between items-center mb-6">
        <div class="flex flex-wrap gap-6">
            <div
                v-for="player in players"
                :key="player.name"
                class="bg-white shadow rounded px-4 py-2 text-center w-40"
            >
                <h3 class="text-lg font-bold">{{ player.name }}</h3>
                <p class="text-2xl font-extrabold">{{ player.score }}</p>
            </div>
        </div>
        <button
            @click="$emit('reset')"
            class="px-4 py-2 bg-red-600 text-white rounded hover:bg-red-500"
        >
            Начать заново
        </button>
    </div>
</template>

<script setup>
const props = defineProps({
    players: Array
})
</script>
