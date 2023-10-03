
<script setup>
</script>
<template>
    --this is slot content--
    <slot> Slot content?? </slot>

    <div>
        <slot name="named-slot">named slot?</slot>
    </div>
    <slot name="named-slot2">named slot 2</slot>
</template>
