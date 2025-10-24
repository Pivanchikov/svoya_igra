<template>
    <div class="fixed inset-0 pointer-events-none overflow-hidden">
        <div
            v-for="n in count"
            :key="n"
            class="absolute text-white opacity-80 select-none"
            :style="flakeStyle(n)"
        >
            ❄
        </div>
    </div>
</template>

<script setup>
    const count = 80

    const flakeStyle = () => {
        const left = Math.random() * 100
        const size = Math.random() * 10 + 10
        const duration = Math.random() * 5 + 5
        const delay = Math.random() * 5

        return {
            left: `${left}vw`,
            fontSize: `${size}px`,
            animation: `fall ${duration}s linear infinite`,
            animationDelay: `${delay}s`,
        }
    }
</script>

<style>
    @keyframes fall {
        0% {
            transform: translateY(0);
        }
        100% {
            transform: translateY(110vh);
        }
    }
</style>
