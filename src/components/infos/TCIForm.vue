<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Target Company Information</h3>    
      <form @submit.prevent="" class="legal-entity-form">
        <div class="form">
          <label>Company Name*</label>
          <input v-model="companyName" type="text" placeholder="Ex: MPC" required>
        </div>
        <div class="form">
          <label>Registration Address</label>
          <input v-model="regAddress" type="text" placeholder="Ex: 123 West End Lane Ikota" required>
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
        <div class="entity-type form">
          <label for="Entity Type">Industry Of The Company*</label>
          <select name="Entity Type" v-model="entityType" required>
            <option value="Private limited liability company">Private limited liability company</option>
            <option value="Public limited liability company">Public limited liability company</option>
          </select>
        </div>
        <div class="form">
          <label>Business Of The Company*</label>
          <textarea v-model="companyBusiness" cols="10" rows="5" placeholder="Ex: 123 West End Lane Ikota" required></textarea>
        </div>
        <div class="form">
          <label>Authorized Share capital of the Company*</label>
          <input v-model="authShares" type="text" placeholder="Ex: 60" required>
        </div>
        <div class="form">
          <label>Price per Share*</label>
          <input v-model="sharePrice" type="number" placeholder="Ex: 70">
        </div>

        <button 
          class="next-btn"
          :disabled="!companyName || !regAddress || !regNo || !regCountry 
          || !definedAs || !companyBusiness || !authShares || !sharePrice"
          @click="nextComp"
        >Next</button>
      </form>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        THIS SHARE SHAREHOLDERS' AGREEMENT is made this ____ day of __________ 20____
      </span>
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
  import { ref } from "vue";

  export default {
    setup (props, context) {
      const companyName = ref("");
      const regAddress = ref("");
      const regNo = ref();
      const regCountry = ref("");
      const definedAs = ref("");
      const entityType = ref();
      const companyBusiness = ref("");
      const authShares = ref("");
      const sharePrice = ref();

      const nextComp = () => {
        context.emit('next')
      }

      return {
        companyName,
        regAddress,
        regNo,
        regCountry,
        definedAs,
        entityType,
        companyBusiness,
        authShares,
        sharePrice,
        nextComp
      }
    }
  }
</script>
