<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Details of the sponsor(s)</h3>
      <br />
      <BaseRadioGroup
        v-model="form.subscriberType"
        name="company"
        :options="subscriberTypes"
      />

      <form
        @submit.prevent=""
        class="legal-entity-form"
        v-if="form.subscriberType === 'Legal Entity'"
      >
        <BaseInput
          v-model="form.companyName"
          label="Company Name"
          type="text"
          placeholder="Ex: MPC"
        />
        <BaseInput
          v-model="form.companyType"
          label="Type Of Company"
          type="text"
          placeholder="Ex: RC Law Firm"
        />
        <BaseTextarea
          v-model="form.address"
          label="Registration Address"
          placeholder="Ex: 123 West End Lane Ikota"
        />
        <BaseInput
          v-model="form.regNo"
          label="Registered Number"
          type="number"
          placeholder="Ex: 1234"
        />
        <BaseInput
          v-model="form.regCountry"
          label="Registration Country"
          type="text"
          placeholder="Ex: Nigeria"
        />
        <BaseInput
          v-model="form.definedAs"
          label="Defined as"
          type="text"
          placeholder="Ex: Main"
        />
        <BaseInput
          v-model="form.preShares"
          label="Pre Completion Shares"
          type="number"
          placeholder="Ex: 10"
        />
        <BaseInput
          v-model="form.postShares"
          label="Post Completion Shares"
          type="number"
          placeholder="Ex: 50"
        />

        <button
          class="next-btn"
          :disabled="
            !form.companyName ||
            !form.companyType ||
            !form.address ||
            !form.regNo ||
            !form.regCountry ||
            !form.definedAs ||
            !form.preShares ||
            !form.postShares
          "
          @click="nextComp"
        >
          Next
        </button>
      </form>

      <form
        @submit.prevent=""
        class="individual-form"
        v-if="form.subscriberType === 'Individual'"
      >
        <BaseInput
          v-model="form.firstName"
          label="First Name"
          type="text"
          placeholder="Ex: Israel"
        />
        <BaseInput
          v-model="form.lastName"
          label="Last Name"
          type="text"
          placeholder="Ex: Oluwapelumi"
        />
        <BaseTextarea
          v-model="form.address"
          label="Address"
          placeholder="Ex: 123 West End Lane Ikota"
        />
        <BaseInput
          v-model="form.definedAs"
          label="Company Name"
          type="text"
          placeholder="Ex: Main"
        />
        <BaseInput
          v-model="form.preShares"
          label="Pre Completion Shares"
          type="number"
          placeholder="Ex: 10"
        />
        <BaseInput
          v-model="form.postShares"
          label="Post Completion Sharese"
          type="number"
          placeholder="Ex: 50"
        />

        <button
          class="next-btn"
          :disabled="
            !form.firstName ||
            !form.lastName ||
            !form.address ||
            !form.definedAs ||
            !form.preShares ||
            !form.postShares
          "
          @click="nextComp"
        >
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
      <span class="fs-6 fw-bold">BY AND AMONG</span>
      <br />
      <br />
      <p>
        , a , incorporated under the laws of with RC Number having its
        registered address at (hereinafter referred to as the “Company” which
        expression shall where the context so permits include its
        successors-in-title and assigns) of the first part;
      </p>

      <span class="fs-6 fw-bold">AND</span>
      <br />
      <br />
      <p v-if="form.subscriberType === 'Legal Entity'">
        <b>{{ form.companyName }}</b
        >, a <b>{{ form.companyType }}</b> company, incorporated under the law of
        <b>{{ form.regCountry }}</b> with RC Number <b>{{ form.regNo }}</b> having its
        registered address at <b>{{ form.address }}</b> currently based in
        (hereinafter referred to as the “Company” which expression shall where
        the context so permits include its successors-in-title and assigns) of
        the second part;
      </p>

      <p v-if="form.subscriberType === 'Individual'">
        <b>{{ form.firstName }}</b> <b>{{ form.lastName }}</b> of
        <b>{{ form.address }}</b> (hereinafter referred to as "" which expression
        shall where the context so admits, include successors-in-title and
        assigns) of the second part;
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
import BaseTextarea from "../inputs/BaseTextarea.vue";

export default {
  components: {
    BaseInput,
    BaseRadioGroup,
    BaseTextarea,
  },
  setup(props, context) {
    const subscriberTypes = ref([
      { label: "Legal Entity", value: "Legal Entity" },
      { label: "Individual", value: "Individual" },
    ]);

    const form = ref({
      subscriberType: "Legal Entity",
      companyName: "",
      companyType: "",
      address: "",
      regNo: "",
      regCountry: "",
      definedAs: "",
      preShares: "",
      postShares: "",
      firstName: "",
      lastName: ""
    });

    const nextComp = () => {
      context.emit("next");
    };

    return {
      subscriberTypes,
      form,
      nextComp,
    };
  },
};
</script>
