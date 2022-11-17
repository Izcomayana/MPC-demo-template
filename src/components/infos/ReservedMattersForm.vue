<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Reserved Matters</h3>    
      <form @submit.prevent="" class="legal-entity-form">
        <div class="form">
          <label>Insert new Reserved Matter*</label>
          <textarea v-model="newReservedMatter" cols="10" rows="5" required></textarea>
        </div>
        <div class="form">
          <label>Insert new Information Right*</label>
          <textarea v-model="newInfo" cols="10" rows="5" required></textarea>
        </div>

        <button class="next-btn" :disabled="!newReservedMatter || !newInfo" @click="nextComp">Next</button>
      </form>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        THIS SHAREHOLDERS' AGREEMENT is made this ____ day of __________ 20____
      </span>
      <br> <br>
      <span class="fs-6 fw-bold">BY AND AMONG</span>
      <br> <br>
      <p>
        <b></b>, a <b></b>, incorporated under the laws of <b></b> with RC Number <b></b> having its registered address at 
        <b></b> (hereinafter referred to as the “Company” which expression shall where the context so permits include its successors-in-title and assigns) 
        of the first part;
      </p>
      <br> <br> <br>
    </div>
  </div>
</template>

<script>
  import { ref } from "vue"

  export default {
    setup (props, context) {
    const newReservedMatter = ref("");
    const newInfo = ref("");

    const nextComp = () => {
      context.emit('next')
    }
  
      return {
        newReservedMatter,
        newInfo,
        nextComp
      }
    }
  }
</script>
