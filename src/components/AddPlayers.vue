<template>
    <div class="max-w-xl mx-auto bg-white shadow p-6 rounded mb-12">
        <h2 class="text-2xl font-bold mb-4">Добавьте участников</h2>
        <div class="flex gap-4 mb-4">
            <input
                :value="newPlayer"
                @input="$emit('update:new-player', $event.target.value)"
                placeholder="Имя игрока"
                class="flex-1 px-4 py-2 border rounded"
                @keyup.enter="submit"
            />
            <button @click="submit" class="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-500">Добавить</button>
        </div>
        <ul class="list-disc list-inside mb-4">
            <li v-for="player in players" :key="player.name">{{ player.name }}</li>
        </ul>
        <button
            v-if="players.length"
            @click="$emit('start')"
            class="mt-2 px-4 py-2 bg-emerald-600 text-white rounded hover:bg-emerald-500"
        >
            Начать игру
        </button>
    </div>
</template>

<script setup>
const props = defineProps({
    players: Array,
    newPlayer: String
})
const emit = defineEmits(['add-player', 'update:new-player', 'start'])

function submit() {
    emit('add-player', props.newPlayer)
    emit('update:new-player', '')
}
</script>
