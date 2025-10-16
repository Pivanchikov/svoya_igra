<template>
    <div class="flex flex-row justify-center flex-wrap gap-4 mb-12">
        <button
            v-for="(round, index) in rounds"
            :key="index"
            @click="$emit('switch', index)"
            class="px-6 py-3 rounded bg-blue-600 hover:bg-blue-500 text-white text-xl font-semibold shadow transition-all duration-200"
            :class="{ 'bg-emerald-600': currentRound === index }"
        >
             {{index === 4 ? 'Финал' : `Тур ${index + 1}`}}
        </button>
    </div>
</template>

<script setup>
const props = defineProps({
    rounds: Array,
    currentRound: Number
})
const emit = defineEmits(['switch'])
</script>
