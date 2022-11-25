<template>
  <div class="form">
    <label>{{ label }}*
    </label>
    <input 
      v-bind="$attrs"
      :value="modelValue" 
      @input="$emit('update:modelValue', $event.target.value)"
      required
    />
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
