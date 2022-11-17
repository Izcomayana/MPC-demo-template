<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Subscription Price</h3>    
      <form @submit.prevent="" class="legal-entity-form">
        <div class="entity-type form">
          <label for="Entity Type">What is the subscription currency?*</label>
          <select name="Entity Type" v-model="selected" required>
            <option value="" disabled selected>Select an option</option>
            <option value="NGN">NGN - Naira</option>
            <option value="USA">$ - United Stated dollars</option>
            <option value="GBP">GBP - Great British Pounds</option>
          </select>
        </div>

        <!-- <div class="entity-type form" v-if="showExchangeRate"> -->
        <div class="entity-type form" v-if="selected !== 'NGN'">
          <label for="Entity Type">What is the agreed exchange rate?*</label>
          <select name="Entity Type">
            <option value="CBN rate published at closing of the Business Day">
              Official Rate of the Central Bank of Nigeria published by the
              Central Bank of Nigeria at closing of the Business Day 
              immediately preceding the relevant date
            </option>
            <option value="CBN rate published at 5pm">
              Official Rate of the Central Bank of Nigeria published by the 
              Central Bank of Nigeria at 5:00 p.m. of the relevant date
            </option>
            <option value="NAFEX published by CBN at closing of the Business Day">
              The Nigerian Autonomous Foreign Exchange Rate Fixing (NAFEX) 
              published by the Central Bank of Nigeria at closing of the 
              Business Day immediately preceding the relevant date
            </option>
            <option value="NAFEX rate published at 5pm">
              The Nigerian Autonomous Foreign Exchange Rate Fixing (NAFEX) 
              published by the Central Bank of Nigeria at 5:00 p.m. of the relevant date
            </option>
            <option value="others">
              Other - applicable rates agreed between the Parties
            </option>
          </select>
        </div>

        <div class="form">
          <label>What is the Subscription Price?*</label>
          <input v-model="subPrice" type="text" placeholder="Ex: $700" required>
        </div>

        <button class="next-btn" :disabled="!subPrice" @click="nextComp">Next</button>
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
      const selected = ref(null);

      const subPrice = ref("");

      const nextComp = () => {
        context.emit('next')
      }

      return {
        selected,
        subPrice,
        nextComp
      }
    }
  }
</script>

<style>
  .entity-type select option {
    width: 5rem;
  }
</style>