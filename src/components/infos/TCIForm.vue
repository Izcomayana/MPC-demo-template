<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Target Company Information</h3>
      <form @submit.prevent="" class="legal-entity-form">
        <BaseInput
          v-model="form.companyName"
          label="Company Name"
          type="text"
          placeholder="Ex: MPC"
        />
        <BaseTextarea
          v-model="form.regAddress"
          label="Registration Address"
          placeholder="Ex: 123 West End Lane Ikota"
        />
        <BaseInput
          v-model="form.regNo"
          label="Registration Number"
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
        <BaseSelect
          :options="entityTypes"
          v-model="form.entityType"
          label="Entity Type"
        />
        <BaseTextarea
          v-model="form.companyBusiness"
          label="Business Of The Company"
          placeholder="Ex: 123 West End Lane Ikota"
        />
        <BaseInput
          v-model="form.authShares"
          label="Authorized Share capital of the Company"
          type="number"
          placeholder="Ex: 60"
        />
        <BaseInput
          v-model="form.sharePrice"
          label="Price per Share"
          type="number"
          placeholder="Ex: 70"
        />

        <button
          class="next-btn"
          :disabled="
            !form.companyName ||
            !form.regAddress ||
            !form.regNo ||
            !form.regCountry ||
            !form.definedAs ||
            !form.companyBusiness ||
            !form.authShares ||
            !form.sharePrice
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
      <p>
        <b>{{ form.companyName }}</b
        >, a <b>{{ form.entityType }}</b
        >, incorporated under the laws of <b>{{ form.regCountry }}</b> with RC Number
        <b>{{ form.regNo }}</b> having its registered address at
        <b>{{ form.regAddress }}</b> (hereinafter referred to as the “Company” which
        expression shall where the context so permits include its
        successors-in-title and assigns) of the first part;
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
import BaseSelect from "../inputs/BaseSelect.vue";
import BaseTextarea from "../inputs/BaseTextarea.vue";

export default {
  components: {
    BaseInput,
    BaseSelect,
    BaseTextarea,
  },
  setup(props, context) {
    const entityTypes = ref([
      "Private limited liability company",
      "Public limited liability company",
    ]);

    const form = ref({
      entityType: null,
      companyName: "",
      regNo: "",
      regAddress: "",
      regCountry: "",
      definedAs: "",
      companyBusiness: "",
      authShares: "",
      sharePrice: ""
    });

    const nextComp = () => {
      context.emit("next");
    };

    return {
      entityTypes,
      form,
      nextComp,
    };
  },
};
</script>
