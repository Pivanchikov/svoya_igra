<template>
    <ul class="garland">
        <li v-for="item in numberLight" :key="item"></li>
    </ul>
</template>

<script setup>
    import {computed} from "vue";

    const widthOneLamp = 40;
    const numberLight = computed(() => Math.floor(window.innerWidth / widthOneLamp));
</script>

<style scoped>
    .garland {
        --globe-width: 12px;
        --globe-height: 28px;
        --globe-spacing: 40px;
        --globe-spread: 3px;
        --light-off-opacity: 0.4;

        top: 0;
        text-align: center;
        white-space: nowrap;
        position: absolute;
        z-index: 1;
        margin: -15px 0 0 0;
        padding: 0;
        pointer-events: none;
        width: 100%;
    }

    .garland li {
        position: relative;
        animation-fill-mode: both;
        animation-iteration-count: infinite;
        list-style: none;
        margin: calc(var(--globe-spacing) / 2);
        padding: 0;
        display: inline-block;
        width: var(--globe-width);
        height: var(--globe-height);
        border-radius: 50%;
        background: rgba(0, 255, 0, 1);
        box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(0, 255, 0, 0.5);
        animation-name: flash-1;
        animation-duration: 2s;
    }

    .garland li:nth-child(2n+1) {
        background: rgba(0, 100, 255, 1);
        box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(0, 100, 255, 0.5);
        animation-name: flash-2;
        animation-duration: 0.4s;
    }

    .garland li:nth-child(3n+2) {
        background: rgba(255, 0, 80, 1);
        box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(255, 0, 80, 0.5);
        animation-name: flash-3;
        animation-duration: 1.1s;
    }

    .garland li:nth-child(4n+2) {
        background: rgba(255, 255, 0, 1);
        box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(255, 255, 0, 0.5);
        animation-name: flash-4;
        animation-duration: 1.1s;
    }

    .garland li:nth-child(odd) {
        animation-duration: 1.8s;
    }

    .garland li:nth-child(3n+1) {
        animation-duration: 1.4s;
    }

    .garland li:before {
        content: "";
        position: absolute;
        background: #222;
        width: calc(var(--globe-width) - 2px);
        height: calc(var(--globe-height) / 3);
        border-radius: 3px;
        top: calc(-1 * (var(--globe-height) / 6));
        left: 1px;
    }

    .garland li:after {
        content: "";
        position: absolute;
        top: calc(-1 * (var(--globe-height) / 2));
        left: calc(var(--globe-width) - 3px);
        width: calc(var(--globe-spacing) + 12px);
        height: calc((var(--globe-height) / 3) * 2);
        border-bottom: solid #222 2px;
        border-radius: 50%;
    }

    .garland li:last-child:after {
        content: none;
    }

    .garland li:first-child {
        margin-left: calc(-1 * var(--globe-spacing));
    }

    /* Keyframes */
    @keyframes flash-1 {
        0%, 100% {
            background: rgba(0, 255, 0, 1);
            box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(0, 255, 0, 1);
        }
        50% {
            background: rgba(0, 255, 0, var(--light-off-opacity));
            box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(0, 255, 0, 0.2);
        }
    }

    @keyframes flash-2 {
        0%, 100% {
            background: rgba(0, 100, 255, 1);
            box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(0, 100, 255, 1);
        }
        50% {
            background: rgba(0, 100, 255, var(--light-off-opacity));
            box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(0, 100, 255, 0.2);
        }
    }

    @keyframes flash-3 {
        0%, 100% {
            background: rgba(255, 0, 80, 1);
            box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(255, 0, 80, 1);
        }
        50% {
            background: rgba(255, 0, 80, var(--light-off-opacity));
            box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(255, 0, 80, 0.2);
        }
    }

    @keyframes flash-4 {
        0%, 100% {
            background: rgba(255, 255, 0, 1);
            box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(255, 255, 0, 1);
        }
        50% {
            background: rgba(255, 255, 0, var(--light-off-opacity));
            box-shadow: 0 calc(var(--globe-height) / 6) calc(var(--globe-width) * 2) var(--globe-spread) rgba(255, 255, 0, 0.2);
        }
    }
</style>
