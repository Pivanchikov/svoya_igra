<template>
    <div class="grid grid-cols-5 gap-6 max-w-7xl mx-auto text-2xl">
        <!-- Темы -->
        <div
            v-for="(theme, themeIndex) in themes"
            :key="'theme-' + themeIndex"
            class="text-center font-bold py-4 bg-blue-100 rounded shadow text-blue-800"
        >
            {{ theme.name }}
        </div>

        <!-- Вопросы -->
        <template v-for="rowIndex in 5">
            <div
                v-for="(theme, themeIndex) in themes"
                :key="'q-' + themeIndex + '-' + rowIndex"
                class="text-center cursor-pointer bg-white hover:bg-blue-100 rounded py-8 font-extrabold shadow-lg transition-transform duration-150 hover:scale-105 border-2 border-blue-300"
                :class="{ 'bg-gray-300 text-gray-500 line-through scale-95 border-dashed': theme.questions[rowIndex - 1].asked }"
                @click="$emit('open-question', themeIndex, rowIndex - 1)"
            >
                {{ theme.questions[rowIndex - 1].price }}
            </div>
        </template>
    </div>
</template>

<script setup>
const props = defineProps({
    themes: Array
})

const emit = defineEmits(['open-question'])
</script>
