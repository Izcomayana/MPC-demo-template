<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Subscription Terms</h3>
      <form @submit.prevent="" class="legal-entity-form">
        <br>
        <label>Will the subscriber be entitled to a director?*</label>
        <div class="d-flex radios" >
          <div class="form-check legal-entity">
            <input 
            @click="directorYes"
            class="form-check-input" 
            id="exampleRadios1" 
            name="exampleRadios" 
            value="yes"
            required
            type="radio" 
            >
            <label class="form-check-label" for="exampleRadios1">
              Yes
            </label>
          </div>
          <div class="form-check">
            <input 
            @click="directorNo"
            class="form-check-input"
            id="exampleRadios2" 
            name="exampleRadios" 
            value="no" 
            type="radio" 
            checked >
            <label class="form-check-label" for="exampleRadios2">
              No
            </label>
          </div>
        </div>

        <div class="form" v-if="showDirectorNo">
          <label>How many Directors will be Subscriber be entitled to?*</label>
          <input type="number" placeholder="Ex: 5" required>
        </div>
        <br>
        <label>Will there be a limit to the number of directors?*</label>
        <div class="d-flex radios">
          <div class="form-check legal-entity">
            <input 
            @click="directorLimitYes"
            class="form-check-input" 
            id="exampleRadios1" 
            name="exampleRadios2" 
            required
            value="yes"
            type="radio" >
            <label class="form-check-label" for="exampleRadios1">
              Yes
            </label>
          </div>
          <div class="form-check">
            <input 
            @click="directorLimitNo"
            class="form-check-input"
            id="exampleRadios2" 
            name="exampleRadios2" 
            value="no" 
            type="radio" 
            checked >
            <label class="form-check-label" for="exampleRadios2">
              No
            </label>
          </div>
        </div>

        <div class="form" v-if="showDirectorLimit">
          <label>What is the limit on the number of directors in the Company*</label>
          <input type="number" placeholder="Ex: 1" required>
        </div>
        <div class="form">
          <label>Insert Subscription Price*</label>
          <input type="number" placeholder="Ex: 500" required>
        </div>
        <br>
        <label>Will the transaction include an anti-dilution clause?</label>
        <div class="d-flex radios">
          <div class="form-check legal-entity">
            <input 
            class="form-check-input" 
            id="exampleRadios1" 
            name="exampleRadios3" 
            value="yes4"
            type="radio" >
            <label class="form-check-label" for="exampleRadios1">
              Yes
            </label>
          </div>
          <div class="form-check">
            <input 
            class="form-check-input"
            id="exampleRadios2" 
            name="exampleRadios3" 
            value="no5" 
            type="radio"
            checked >
            <label class="form-check-label" for="exampleRadios2">
              No
            </label>
          </div>
        </div> 

        <button>Next</button>
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
      const selected = ref();
        // const ariaDescribedby = ref("A")

        const showDirectorNo = ref(false)

        const directorYes = () => {
          showDirectorNo.value = true
        }

        const directorNo = () => {
          showDirectorNo.value = false
        }

        const showDirectorLimit = ref(false)

        const directorLimitYes = () => {
          showDirectorLimit.value = true
        }

        const directorLimitNo = () => {
          showDirectorLimit.value = false
        }

        // const entitledDirNo = ref()

      return {
        selected,
        showDirectorNo,
        directorYes,
        directorNo,
        showDirectorLimit,
        directorLimitYes,
        directorLimitNo
      }
    }
  }

  
</script>

<style>
  /* .radios {
    margin-top: 0;
  }

  .legal-entity {
    margin-right: 2rem;
  }

  .legal-entity-form {
    margin-top: 1rem;
  }

  .entity-type {
    display: flex;
    flex-direction: column;
  }

  .entity-type label {
    margin-bottom: 0.25rem;
  }

  .entity-type select {
    width: 16rem;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid rgb(92, 92, 92);
    font-size: 0.9rem;
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