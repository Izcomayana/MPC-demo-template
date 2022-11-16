<template>
  <div class="select-comp">
    <p>Select components</p>
    <select v-model="selected">
    <option v-for="option in options" :key="option" :value="option.value">
      {{ option.text }}
    </option>
  </select>

  <div>Selected: {{ selected }}</div>

  </div>
</template>

<script>
  import { ref } from 'vue'
  
  export default {
    setup () {
      const selected = ref('A')

      const options = ref([
        { text: 'One', value: 'A' },
        { text: 'Two', value: 'B' },
        { text: 'Three', value: 'C' }
      ])

      return {
        selected,
        options
      }
    }
  }
</script>

<style>

</style>