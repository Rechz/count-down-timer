<template>
    <div v-if="!isPara" class="text-center">
        <h3 class="head mb-3">Enter Number</h3>
        <i class='fa-solid fa-hand-point-down icon mb-3'></i>
    </div>
    <div v-else class="text-center">
        <h3 class="head mb-3">Counting down...</h3>
        <i class='fas fa-stopwatch icon mb-3'></i>
    </div>
</template>

<script>
export default {
    props : ['isPara']
}
</script>