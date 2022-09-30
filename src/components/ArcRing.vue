<script setup lang="ts">
import {computed, ref} from "vue";

const props = defineProps({
    start: {type: Number, required: true},
    stop: {type: Number, required: true},
    ro: {type: Number, required: true},
    ri: {type: Number, required: true},
    name: {type: String, required: true},
});

const outerStop = computed(() => {
    return {
        x: Math.cos(props.stop * Math.PI / 180) * outerR.value,
        y: Math.sin(props.stop * Math.PI / 180) * outerR.value
    }
})

const outerStart = computed(() => {
    return {
        x: Math.cos(props.start * Math.PI / 180) * outerR.value,
        y: Math.sin(props.start * Math.PI / 180) * outerR.value
    }
})

const innerStop = computed(() => {
    return {
        x: Math.cos(props.stop * Math.PI / 180) * innerR.value,
        y: Math.sin(props.stop * Math.PI / 180) * innerR.value
    }
})

const innerStart = computed(() => {
    return {
        x: Math.cos(props.start * Math.PI / 180) * innerR.value,
        y: Math.sin(props.start * Math.PI / 180) * innerR.value
    }
})

const outerR = ref(props.ro)
const innerR = ref(props.ri)

const center = computed((): { x: number, y: number } => {
    return {
        x: (outerStop.value.x + outerStart.value.x + innerStop.value.x + innerStart.value.x) / 4,
        y: (outerStop.value.y + outerStart.value.y + innerStop.value.y + innerStart.value.y) / 4
    };
})

</script>

<template lang="pug">
g.pie
    path.main(:d="`M ${innerStop.x} ${innerStop.y} L ${outerStop.x} ${outerStop.y} A ${outerR} ${outerR} 0 0 1 ${outerStart.x} ${outerStart.y} L ${innerStart.x} ${innerStart.y} A ${innerR} ${innerR} 1 0 0 ${innerStop.x} ${innerStop.y} `" fill="pink" stroke="grey" stroke-width="2")
    //g(style="`transform: translate(0,  0.5rem);`")
    text.name(v-text="props.name" :x="center.x" :y="center.y" :style="`transform-origin: ${center.x}px ${center.y}px;`")
</template>

<style scoped lang="less">
g.pie * {
    vector-effect: non-scaling-stroke;
}

path.main {
    fill: lightblue;
    &:hover {
        fill: lightgreen;
    }
}

g.pie {
    &:hover {
        text {
            font-weight: bolder;
        }
    }
}

text.name {
    user-select: none;
    pointer-events: none;
    -webkit-user-drag: none;

    text-anchor: middle;
    transform: rotate(105deg);
}
</style>