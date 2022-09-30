<template lang="pug">
svg(width="640" height="500" viewBox="-320 -250 640 500")
    circle(cx="0" cy="0" r="240" stroke="black" stroke-width="1" fill="white")
    circle(cx="0" cy="0" r="160" stroke="black" stroke-width="1" fill="white")
    circle(cx="0" cy="0" r="80" stroke="black" stroke-width="1" fill="white")
    g.c-center
        g(v-for="(n, $index) in names_major")
            ArcRing(:stop="$index * 30" :start="($index + 1) * 30" :ro="240" :ri="160" :name="n")
        g(v-for="(n, $index) in names_minor")
            ArcRing(:stop="$index * 30" :start="($index + 1) * 30" :ro="160" :ri="80" :name="n")

</template>

<script setup lang="ts">
import ArcRing from './ArcRing.vue';

const names_major = ['C', 'G', 'D', 'A', 'E', 'B', 'G♭/F#', 'D♭', 'A♭', 'E♭', 'B♭', 'F'];
const names_minor = ['Am', 'Em', 'Bm', 'F#m', 'C#m', 'G#m', 'E♭m,/D#m', 'B♭m', 'Fm', 'Cm', 'Gm', 'Dm'];

</script>

<style scoped lang="less">
svg {
    outline: 1px solid grey;
}

g.c-center {
    transform: rotate(-105deg);
}
</style>