<template>
    <div class="space-y-4">
        <!-- Вопрос -->
        <div>
            <template v-for="(item, index) in normalize(question.question)" :key="'q-' + index">
                <component
                    v-if="isMedia(item)"
                    :is="mediaComponent(item)"
                    :src="getMediaUrl(item)"
                    class="max-w-full rounded mb-2"
                    controls
                />
                <p v-else class="text-lg mb-2">{{ item }}</p>
            </template>
        </div>

        <!-- Ответ -->
        <div v-if="showAnswer" class="border-t border-zinc-600 pt-4">
            <h3 class="font-semibold mb-2">Ответ</h3>
            <template v-for="(item, index) in normalize(question.answer)" :key="'a-' + index">
                <component
                    v-if="isMedia(item)"
                    :is="mediaComponent(item)"
                    :src="getMediaUrl(item)"
                    class="max-w-full rounded mb-2"
                    controls
                />
                <p v-else class="text-lg mb-2">{{ item }}</p>
            </template>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    question: Object,
    showAnswer: Boolean
})

const isMedia = (val) => typeof val === 'string' && /\.(jpg|jpeg|png|gif|webp|mp3|wav|ogg|mp4|webm)$/i.test(val)
const getMediaUrl = (path) => `/src/assets/${path}`
const mediaComponent = (val) => {
    if (typeof val !== 'string') return 'div'
    if (val.match(/\.(jpg|jpeg|png|gif|webp)$/i)) return 'img'
    if (val.match(/\.(mp4|webm)$/i)) return 'video'
    if (val.match(/\.(mp3|wav|ogg)$/i)) return 'audio'
    return 'div'
}

// Нормализация: превращает строку в массив, если надо
const normalize = (val) => Array.isArray(val) ? val : [val]
</script>

<style scoped>
video, img {
    max-height: 400px;
}
</style>
