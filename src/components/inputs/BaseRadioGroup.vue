<template>
  <label v-if="label">{{ label }}*</label>
  <span class="d-flex radios">
    <component
      v-for="option in options"
      :key="option.value"
      :is="vertical ? 'div' : 'span'"
      :class="{
        'form-check legal-entity': !vertical
      }"
    >
      <BaseRadio 
        :label="option.label"
        :value="option.value" 
        :name="name"
        :modelValue="modelValue"
        @update:modelValue="$emit('update:modelValue', $event)"
        class="form-check-input "
        id="exampleRadios1"
      />
    </component>
  </span>
    
  
  
</template>

<script>
  import BaseRadio from './BaseRadio.vue';
  export default {
    components: {
      BaseRadio
    },
    props: {
      label: {
        type: String,
        default: ""
      },
      options: {
        type: Array,
        required: true
      },
      modelValue: {
        type: [String, Number],
        default: ""
      },
      name: {
        type: String,
        required: true 
      },
      vertical: {
        type: Boolean,
        default: false
      }
    }
  }
</script>

<style>
  .form {
    margin-bottom: 1rem;
  }
</style>
