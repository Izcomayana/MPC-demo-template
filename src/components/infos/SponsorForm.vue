<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Details of the sponsor(s)</h3>
      <br>
      <div class="d-flex radios">
        <div class="form-check legal-entity">
          <input 
          @click="legalEntity"
          class="form-check-input" 
          id="exampleRadios1" 
          name="exampleRadios" 
          value="legalEntity"
          type="radio" 
          checked >
          <label class="form-check-label" for="exampleRadios1">
            Legal Entity
          </label>
        </div>
        <div class="form-check">
          <input 
          @click="individual"
          class="form-check-input"
          id="exampleRadios2" 
          name="exampleRadios" 
          value="individual" 
          type="radio" >
          <label class="form-check-label" for="exampleRadios2">
            Individual
          </label>
        </div>
      </div>
      
      <form @submit.prevent="" class="legal-entity-form" v-if="showlegalEntityForm">
        <div class="form">
          <label>Company Name*</label>
          <input v-model="companyName" type="text" placeholder="Ex: MPC" required>
        </div>
        <div class="form">
          <label>Type Of Company*</label>
          <input v-model="companyType" type="text" placeholder="Ex: RC Law Firm">
        </div>
        <div class="form">
          <label>Registration Address</label>
          <textarea cols="10" v-model="address" rows="5" placeholder="Ex: 123 West End Lane Ikota" required></textarea>
        </div>
        <div class="form">
          <label>Registered Number*</label>
          <input v-model="regNo" type="number" placeholder="Ex: 1234" required>
        </div>
        <div class="form">
          <label>Registration Country*</label>
          <input v-model="regCountry" type="text" placeholder="Ex: Nigeria" required>
        </div>
        <div class="form">
          <label>Defined as*</label>
          <input v-model="definedAs" type="text" placeholder="Ex: Main" required>
        </div>
        <div class="form">
          <label>Pre Completion Shares*</label>
          <input v-model="preShares" type="number" placeholder="Ex: 10" required>
        </div>
        <div class="form">
          <label>Post Completion Shares*</label>
          <input v-model="postShares" type="number" placeholder="Ex: 60" required>
        </div>

        <button 
          class="next-btn"
          :disabled="!companyName || !companyType || !address 
          || !regNo || !regCountry || !definedAs || !preShares || !postShares"
          @click="nextComp"
          >Next</button>
      </form>

      <form @submit.prevent="" class="individual-form" v-if="showIndividualForm">
        <div class="form">
          <label>First Name*</label>
          <input v-model="firstName" type="text" placeholder="Ex: Israel" required>
        </div>
        <div class="form">
          <label>Last Name*</label>
          <input v-model="lastName" type="text" placeholder="Ex: Oluwapelumi" required>
        </div>
        <div class="form">
          <label>Address*</label>
          <textarea v-model="address" cols="10" rows="5" placeholder="Ex: 123 West End Lane Ikota" required></textarea>
        </div>
        <div class="form">
          <label>Defined as*</label>
          <input v-model="definedAs" type="text" placeholder="Ex: Main" required>
        </div>
        <div class="form">
          <label>Pre Completion Shares*</label>
          <input v-model="preShares" type=" number" placeholder="Ex: 10" required>
        </div>
        <div class="form">
          <label>Post Completion Shares*</label>
          <input v-model="postShares" type=" number" placeholder="Ex: 60" required>
        </div>

        <button 
        class="next-btn"
        :disabled="!firstName || !lastName || !address || !definedAs || !preShares || !postShares" 
        @click="nextComp">Next</button>
      </form>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        THIS SHARE SHAREHOLDERS' AGREEMENT is made this ____ day of __________ 20____
      </span>
      <br> <br>
      <span class="fs-6 fw-bold">BY AND AMONG</span>
      <br> <br>
      <p>
        , a , incorporated under the laws of with RC Number having its registered address at 
        (hereinafter referred to as the “Company” which expression shall where the context so permits include its successors-in-title and assigns) 
        of the first part;
      </p>
      
      <span class="fs-6 fw-bold">AND</span>
      <br> <br>
      <p v-if="showlegalEntityForm">
        <b>{{ companyName }}</b>, a <b>{{ companyType }}</b> company, incorporated under the law of 
        <b>{{ regCountry }}</b> with RC Number <b>{{ regNo }}</b> having its registered address at 
        <b>{{ address }}</b> currently based in  (hereinafter referred to as the “Company” which expression 
        shall where the context so permits include its successors-in-title and assigns) of the second part;
      </p> 
      
      <p v-if="showIndividualForm">
        <b>{{ firstName }}</b> <b>{{ lastName }}</b> of <b>{{ address }}</b> (hereinafter referred to as "" which expression shall where the context so admits, 
        include successors-in-title and assigns) of the second part;
      </p>
      <br> <br> <br>
    </div>
  </div>
</template>

<script>
  import { ref } from "@vue/reactivity"

  export default {
    setup (props, context) {
      const showlegalEntityForm = ref(true);
      const showIndividualForm = ref(false);

      const legalEntity = () => {
        showlegalEntityForm.value = true;
        showIndividualForm.value = false;
      }

      const individual = () => {
        showlegalEntityForm.value = false;
        showIndividualForm.value = true;
      }

      const companyName = ref("");
      const companyType = ref("");
      const address = ref("");
      const regNo = ref();
      const regCountry = ref("");
      const definedAs = ref("");
      const preShares = ref();
      const postShares = ref();

      const nextComp = () => {
        context.emit('next')
      }
      
      const firstName = ref("");
      const lastName = ref("");

      return {
        showlegalEntityForm,
        showIndividualForm,
        legalEntity,
        individual,
        companyName,
        companyType,
        address,
        regNo,
        regCountry,
        definedAs,
        preShares,
        postShares,
        firstName,
        lastName,
        nextComp
      }
    }
  }
</script>
