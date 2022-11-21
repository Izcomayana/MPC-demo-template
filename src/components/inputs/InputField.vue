<template>
  <div class="form">
    <label> label: {{ label }}*
      <i class="bi bi-info-circle-fill icon" data-bs-toggle="modal" data-bs-target="#exampleModal"></i>
    </label>
    <input type="text" v-model="entityName" placeholder="Ex: My Pocket Counsel" required>
  </div>
</template>

<script>
  import { ref } from "vue";

  export default {
    props: ["label"],
    setup () {
      // const label = ref("Entity Name");
      
      // return {
      //   label
      // }
    }
  }
</script>

<style>

</style>