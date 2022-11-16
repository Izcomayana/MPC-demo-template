<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Shareholders</h3>    
      <form @submit.prevent="" class="legal-entity-form">
        <div class="form">
          <label>Name*</label>
          <input v-model="name" type="text" placeholder="Ex: Oluwapelumi Sotoyinbo" required>
        </div>
        <div class="form">
          <label>Address</label>
          <textarea v-model="address" cols="10" rows="5" placeholder="Ex: 123 West End Lane Ikota" required></textarea>
        </div>
        <div class="form">
          <label>Shareholding*</label>
          <input v-model="shareholding" type="text" required>
        </div>

        <button :disabled="!name || !address || !shareholding">Next</button>
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
      const name = ref("");
      const address = ref("");
      const shareholding = ref("");

      return {
        name,
        address,
        shareholding
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

  .entity-type {
    display: flex;
    flex-direction: column;
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