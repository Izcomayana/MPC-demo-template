<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Subscription Price</h3>
      <form @submit.prevent="" class="legal-entity-form">
        <BaseSelect
          :options="currencies"
          v-model="form.currency"
          label="What is the subscription currency"
        />

        <div class="entity-type form">
          <BaseSelect
            :options="exchangeRates"
            v-model="form.exchangeRate"
            label="What is the subscription currency"
            v-if="
              form.currency === '$ - United Stated dollars' ||
              form.currency === 'GBP - Great British Pounds'
            "
          />
        </div>

        <BaseInput
          v-model="form.subPrice"
          label="What is the Subscription Price?"
          type="number"
          placeholder="Ex: 700"
        />

        <button class="next-btn" :disabled="!form.subPrice" @click="nextComp">
          Next
        </button>
      </form>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        THIS SHARE SHAREHOLDERS' AGREEMENT is made this ____ day of __________
        20____
      </span>
      <br />
      <br />
      <p>“Subscription Price” means <b>{{ form.subPrice }}</b></p>
      <br />
      <br />
      <br />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

import BaseInput from "../inputs/BaseInput.vue";
import BaseSelect from "../inputs/BaseSelect.vue";

export default {
  components: {
    BaseInput,
    BaseSelect,
  },
  setup(props, context) {
    const currencies = ref([
      "NGN - Naira",
      "$ - United Stated dollars",
      "GBP - Great British Pounds",
    ]);

    const exchangeRates = ref([
      "Official Rate of the Central Bank of Nigeria published by the Central Bank of Nigeria at closing of the Business Day immediately preceding the relevant date",
      "Official Rate of the Central Bank of Nigeria published by the Central Bank of Nigeria at 5:00 p.m. of the relevant date",
      "The Nigerian Autonomous Foreign Exchange Rate Fixing (NAFEX) published by the Central Bank of Nigeria at closing of the Business Day immediately preceding the relevant date",
      "The Nigerian Autonomous Foreign Exchange Rate Fixing (NAFEX) published by the Central Bank of Nigeria at 5:00 p.m. of the relevant date",
      "Other - applicable rates agreed between the Parties",
    ]);

    const form = ref({
      currency: "",
      exchangeRate: "",
      subPrice: "",
    });

    const nextComp = () => {
      context.emit("next");
    };

    return {
      currencies,
      exchangeRates,
      form,
      nextComp,
    };
  },
};
</script>

<style>
.entity-type select option {
  width: 5rem;
}
</style>