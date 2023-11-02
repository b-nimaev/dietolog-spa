<script setup lang="ts">
const route = useRoute()

// When accessing /posts/1, route.params.id will be 1
console.log(route.params.id)
</script>

<template>
    <div class="container">
        <h1>{{ route.params.id }}</h1>
    </div>
</template>
