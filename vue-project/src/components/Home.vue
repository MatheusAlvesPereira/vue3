<template>
    <h1>home</h1>

    <button>{{ onClick }}</button>
</template>

<script setup>
    import { ref } from 'vue'

    const onClick = ref(() => {
        console.log('click')
    })
</script>