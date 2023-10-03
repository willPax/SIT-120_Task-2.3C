<script setup>
defineEmits(['changeColourChild'])
defineProps(['myprops'])
</script>

<template>
    <div >
        <p>
            <h3>This is the child component</h3>
            this is the props: {{ myprops }} <br>
            this is the button working from the child component using emit
            <button @click="$emit('changeColourChild')"> click to change colour</button>
        </p>
    </div>

</template>