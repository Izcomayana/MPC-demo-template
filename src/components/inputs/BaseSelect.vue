<template>
  <div class="entity-type">
    <label for="Entity Type">{{ label }}</label>
    <select 
      :value="modelValue"
      name="Entity Type"
      v-bind="{ 
        ...$attrs, onChange: ($event) => { $emit('update:modelValue', $event.target.value) }
      }">
      <option 
        v-for="option in options"
        :key="option"
        :value="option"
        :selected="option === modelValue"
        >{{ option }}
      </option>
    </select>
  </div>
</template>

<script>
  import { ref } from "vue";

  export default {
    props: {
      label: {
        type: String,
        default: ""
      },
      modelValue: {
        type: [String, Number],
        default: ""
      },
      options: {
        type: Array,
        required: true
      }
    }
  }
</script>

<style>

</style>