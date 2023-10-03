<template>
    <div class="nice-class">
        <p>this is the id: {{ id }} </p>
        <p>this is the name: {{ name }}</p>
        <p>this is the items index: {{ index }}</p>
    </div>
</template>

<script setup>

defineProps(['id', 'name', 'index'])

</script>

<style scoped>
.nice-class {
    background-color: rgb(248, 202, 210);
    color: rgb(226, 148, 4);
}

</style>