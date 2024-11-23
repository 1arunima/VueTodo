
<script setup>


import {ref} from "vue"
 const array = ref(["orange", "apple", "mango"])

 function removeItem (index){
    array.value.splice(index,1)
 }


</script>



<template>
    <div>
        <ul>
        
      <li v-for="(item, index) in array" :key="index">
      {{ item }}

      <button @click="removeItem(index)">Remove</button>
      </li>
        </ul>
    </div>
</template>


<style lang="scss" scoped>

</style>