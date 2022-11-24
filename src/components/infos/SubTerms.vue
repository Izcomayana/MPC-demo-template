<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Subscription Terms</h3>
      <form @submit.prevent="" class="legal-entity-form">
        <br />
        <BaseRadioGroup
          v-model="form.director"
          name="director"
          :options="directors"
          label="Will the subscriber be entitled to a director?"
        />
        <BaseInput
          v-model="form.noOfDirector"
          label="How many Directors will be Subscriber be entitled to?"
          type="number"
          placeholder="Ex: 5"
          v-if="form.director === 'Yes'"
        />
        <br />
        <BaseRadioGroup
          v-model="form.directorLimit"
          name="director limit"
          :options="directors"
          label="Will there be a limit to the number of directors?"
        />
        <BaseInput
          v-model="form.noOfDirectorLimit"
          label="What is the limit on the number of directors in the Company?"
          type="number"
          placeholder="Ex: 1"
          v-if="form.directorLimit === 'Yes'"
        />
        
        <BaseInput
          v-model="form.subPrice"
          label="Insert Subscription Price?"
          type="number"
          placeholder="Ex: 500"
        />
        <br />
        <BaseRadioGroup
          v-model="form.antiDilution"
          name="director limit"
          :options="directors"
          label="Will the transaction include an anti-dilution clause?"
        />

        <button class="next-btn" :disabled="!subPrice" @click="nextComp">
          Next
        </button>
      </form>
    </div>

    <div class="agreement-sheet" v-if="form.antiDilution === 'Yes'">
      <span class="fs-6 fw-bold" >Anti-Dilution</span>
      <br />
      <br />
      <p>
        It is hereby agreed that the Subscriber shall at all times be protected
        against dilution of its shareholding in the Company
      </p>
      <p>
        If the Company issues any new shares after the Completion Date, which
        are priced on the basis of a pre-money valuation of the Company that is
        lower than the post-money valuation relating the investment made by the
        Subscriber, the Company shall, unless and to the extent that the
        Subscriber shall have specifically waived its rights under this
        paragraph in writing, issue to the Subscriber, at no extra cost to the
        Subscriber, such number of shares to the extent that the Subscriber
        shall after such allotment hold not less than 13% (thirteen percent) of
        the Company’s share capital
      </p>
      <br />
      <br />
      <br />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

import BaseInput from "../inputs/BaseInput.vue";
import BaseRadioGroup from "../inputs/BaseRadioGroup.vue";

export default {
  components: {
    BaseInput,
    BaseRadioGroup
  },
  setup(props, context) {
    const directors = ref([
      { label: 'Yes', value: "Yes"},
      { label: 'No', value: "No"}
    ])

    const form = ref({
      director: "No",
      noOfDirector: "",
      directorLimit: "No",
      noOfDirectorLimit: "",
      subPrice: "",
      antiDilution: "No"
    })

    const nextComp = () => {
      context.emit("next");
    };

    return {
      directors,
      form,
      nextComp,
    };
  },
};
</script>
