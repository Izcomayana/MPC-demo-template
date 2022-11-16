<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Subscription Price</h3>    
      <form @submit.prevent="" class="legal-entity-form">
        <div class="entity-type form">
          <label for="Entity Type">What is the subscription currency?*</label>
          <select name="Entity Type" v-model="selected" required>
            <option value="" disabled selected>{{ selectedText }}</option>
            <option value={NGN}>NGN - Naira</option>
            <option @click="exchangeRate"  value={USA} selected>$ - United Stated dollars</option>
            <option @click="exchangeRate" value={GBP}>GBP - Great British Pounds</option>
          </select>
        </div>

        <!-- <selectInput :options="newOptions" /> -->

        <div class="entity-type form" v-if="showExchangeRate">
          <label for="Entity Type">What is the subscription currency?*</label>
          <select name="Entity Type">
            <option value="NGN - Naira">NGN - Naira</option>
            <option value="$ - United Stated dollars">$ - United Stated dollars</option>
            <option value="GBP - Great British Pounds">GBP - Great British Pounds</option>
          </select>
        </div>

        <div class="form">
          <label>What is the Subscription Price?*</label>
          <input v-model="subPrice" type="text" placeholder="Ex: $700">
        </div>

        <button :disabled="!subPrice" class="next-btn">Next</button>
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

  import selectInput from "../inputs/Select.vue";

  export default {
    components: {
      selectInput
    },
    setup () {
      const selected = ref(null);
      const selectedText = ref("Select an option");

      const showExchangeRate = ref(false)

      const exchangeRate = () => {
        showExchangeRate.value = true
      }

      const subPrice = ref();

      const newOptions = ref([
        { text: 'Four', value: 'D' },
        { text: 'Five', value: 'E' },
        { text: 'Six', value: 'F' }
      ])
      return {
        newOptions,
        selected,
        selectedText,
        showExchangeRate,
        exchangeRate,
        subPrice
      }
    }
  }
</script>
