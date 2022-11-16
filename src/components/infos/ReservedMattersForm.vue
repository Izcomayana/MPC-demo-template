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

        <button :disabled="!newReservedMatter || !newInfo" class="next-btn">Next</button>
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
        <b>{{ companyName }}</b>, a <b>{{ entityType }}</b>, incorporated under the laws of <b>{{ regCountry }}</b> with RC Number <b>{{ regNo }}</b> having its registered address at 
        <b>{{ regAddress}}</b> (hereinafter referred to as the “Company” which expression shall where the context so permits include its successors-in-title and assigns) 
        of the first part;
      </p>
      <br> <br> <br>
    </div>
  </div>
</template>

<script>
  import { ref } from "vue"

  export default {
    setup () {
    const newReservedMatter = ref("");
    const newInfo = ref("");
  
      return {
        newReservedMatter,
        newInfo
      }
    }
  }
</script>

<style>
  /* .legal-entity {
    margin-right: 2rem;
  }

  .legal-entity-form {
    margin-top: 1rem;
  }
  
  .form {
    margin-top: 1rem;
    display: flex;
    flex-direction: column;
  }

  .form label {
    margin-bottom: 0.25rem;
  }

  .form input {
    width: 16rem;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid rgb(92, 92, 92);
    font-size: 0.9rem;
  }

  .form textarea {
    padding: 10px;
    border-radius: 5px;
    border: 1px solid rgb(92, 92, 92);
    width: 75%;
  } */
</style>