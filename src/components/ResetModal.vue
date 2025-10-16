<template>
    <div class="fixed inset-0 bg-black bg-opacity-60 flex items-center justify-center z-50">
        <div class="bg-white p-6 rounded max-w-md w-full text-gray-900 shadow-xl">
            <h2 class="text-xl font-bold mb-4">Начать игру заново?</h2>
            <p class="mb-6">Все участники, очки и прогресс будут удалены. Вы уверены?</p>
            <div class="flex justify-end gap-4">
                <button class="px-4 py-2 bg-gray-200 rounded hover:bg-gray-300" @click="$emit('cancel')">Отмена</button>
                <button class="px-4 py-2 bg-red-600 text-white rounded hover:bg-red-500" @click="$emit('confirm')">Подтвердить</button>
            </div>
        </div>
    </div>
</template>

<script setup>
const emit = defineEmits(['confirm', 'cancel'])
</script>
