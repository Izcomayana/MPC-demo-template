<template>
  <div class="form">
    <label>{{ label }}*
    </label>
    <textarea 
      cols="30" 
      rows="5"
      v-bind="$attrs"
      :value="modelValue" 
      @input="$emit('update:modelValue', $event.target.value)">
    </textarea>
  </div>
</template>

<script>
  export default {
    props: {
      label: {
        type: String,
        default: ""
      },
      modelValue: {
        type: [String, Number],
        default: ""
      }
    }
  }
</script>
