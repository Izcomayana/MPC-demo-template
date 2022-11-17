<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Disclosed Agreement</h3>    
      <form @submit.prevent="" class="legal-entity-form">
        <div class="form">
          <label>Agreement description*</label>
          <textarea v-model="agreementDescription" cols="10" rows="5" required></textarea>
        </div>
        <button class="next-btn" type="submit" @click="addDisclosure">Insert Condition <i class="bi bi-forward"></i></button>
      </form>
      <button class="next-btn" :disabled="!agreementDescription" @click="nextComp">Next</button>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        10. SPECIFIC INDEMNITIES
      </span>
      <br> <br>
      <p>
        10.1 Notwithstanding any Disclosures made, the Sponsors shall indemnify the Investor and 
        keep it indemnified against all Losses suffered by the Investor or the Company whatsoever 
        (together with all costs (including legal and settlement costs), charges, interest, 
        penalties and expenses relating thereto), and shall pay to the Investor a sum equal 
        thereto and/or make appropriate and proportionate adjustments to the entry valuation, 
        as a result of or in connection with:
      </p>
      <div v-for="(disclosure, index) in disclosures" :key="index">
        <p>{{ index + 11.1 }} {{ disclosure.description }}</p>
      </div>
      <br> <br> <br>
    </div>
  </div>
</template>

<script>
  import { ref } from "vue"

  export default {
    setup (props, context) {
      const agreementDescription = ref("");

      const nextComp = () => {
        context.emit('next')
      }

      const disclosures = ref([
        { description: "breach of a Tax Covenant or Tax Warranty" }
      ]);

      const addDisclosure = () => {
        if (agreementDescription !== "") {
          disclosures.value.push({
            description: agreementDescription.value
          })
        }
      }

      return {
        agreementDescription,
        nextComp,
        disclosures,
        addDisclosure
      }
    }
  }
</script>
