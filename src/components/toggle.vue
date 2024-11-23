

<script setup>
 

 import {ref} from "vue"

 const isvisible =ref(true)


 function toggleVisible() {
     isvisible.value= !isvisible.value
 }

</script>

<template>
    <div>
        <button @click="toggleVisible">go an toggle</button>
        <p v-if="isvisible"> toggle is working??????</p>
    </div>
</template>

<style lang="scss" scoped>


</style>