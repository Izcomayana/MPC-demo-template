<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-3 pt-3 rounded">
      <h3>Details of the subscriber</h3>
      <br />
      <BaseRadioGroup
        v-model="form.subscriberType"
        name="company type"
        :options="subscriberTypes"
      />

      <form
        @submit.prevent=""
        class="legal-entity-form"
        v-if="form.subscriberType === 'Legal Entity'"
      >
        <BaseSelect
          :options="entityTypes"
          v-model="form.entityType"
          label="Entity Type"
        />
        <div class="form">
          <label
            >Entity Name*
            <i
              class="bi bi-info-circle-fill icon"
              data-bs-toggle="modal"
              data-bs-target="#exampleModal"
            ></i>
          </label>
          <input
            type="text"
            v-model="form.entityName"
            placeholder="Ex: My Pocket Counsel"
            required
          />
        </div>

        <!-- Modal -->
        <div
          class="modal fade"
          id="exampleModal"
          tabindex="-1"
          aria-labelledby="exampleModalLabel"
          aria-hidden="true"
        >
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h1 class="modal-title fs-5" id="exampleModalLabel">
                  Drafting Note
                </h1>
                <button
                  type="button"
                  class="btn-close"
                  data-bs-dismiss="modal"
                  aria-label="Close"
                ></button>
              </div>
              <div class="modal-body">
                <p>
                  The Company and the Sponsors will typically raise the argument
                  that the agreement is primarily between the Company who is
                  issuing the shares and Investor who is subscribing for the
                  shares, hence, there is no need for the Sponsors to be a party
                  to the Agreement. Furthermore, that based on the principle of
                  separate corporate personality pursuant to Section 42 of the
                  CAMA they should not be made a party or be liable under the
                  Agreement. The Investor can rebut this position on several
                  grounds. Firstly, that while the Company is a separate entity
                  it is an artificial person that acts through natural persons
                  like the Sponsors who are in charge of the daily operations
                  and policies of the Company. Secondly, in the event of a
                  warranty breach and the Investor makes a claim for breach of
                  warranties such a claim is equal to the Investor receiving its
                  invested funds without the projected returns on investment.
                </p>
                <br />
                <br />
                <p>
                  Thirdly, the investment is most times predicated on business
                  plans prepared by the Sponsors and the Investor is relying on
                  the Sponsors for implementation based on the representations
                  and assurances giving by the Sponsors. As such, the Investor
                  is asking the Sponsor to put their money where their mouth is.
                  Ultimately, the negotiations depends on the bargaining
                  strength of the parties. Where the Sponsor is made a party to
                  the Agreement, the Sponsor can rely on several risk mitigating
                  mechanisms discussed below.
                </p>
              </div>
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-secondary next-btn"
                  data-bs-dismiss="modal"
                >
                  Close
                </button>
              </div>
            </div>
          </div>
        </div>

        <BaseInput
          v-model="form.regNo"
          label="Registration Number"
          type="number"
          placeholder="Ex: 1234"
        />
        <BaseTextarea
          v-model="form.regAddress"
          label="Registration Number"
          placeholder="Ex: 123 West End Lane Ikota"
        />
        <BaseInput
          v-model="form.regCountry"
          label="Registration Country"
          type="text"
          placeholder="Ex: Nigeria"
        />
        <BaseInput
          v-model="form.PostShares"
          label="Post Completion Shares"
          type="number"
          placeholder="0"
        />

        <button
          :disabled="
            !form.entityName || !form.regNo || !form.regAddress || !form.regCountry || !form.PostShares
          "
          @click="nextComp"
          class="next-btn"
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
          v-model="form.regAddress"
          label="Address"
          placeholder="Ex: 123 West End Lane Ikota"
        />
        <BaseInput
          v-model="form.PostShares"
          label="Post Completion Shares"
          type="number"
          placeholder="0"
        />

        <button
          class="next-btn"
          :disabled="!form.firstName || !form.lastName || !form.PostShares"
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
      <p  v-if="form.subscriberType === 'Legal Entity'">
        <b>{{ form.entityName }}</b
        >, a <b>{{ form.entityType }}</b
        >, incorporated under the laws of <b>{{ form.regCountry }}</b> with RC Number
        <b>{{ form.regNo }}</b> having its registered address at
        <b>{{ form.regAddress }}</b> (hereinafter referred to as the “Company” which
        expression shall where the context so permits include its
        successors-in-title and assigns) of the first part;
      </p>
      <p v-if="form.subscriberType === 'Individual'">
        <b>{{ form.firstName }}</b> <b>{{ form.lastName }}</b> of
        <b>{{ form.regAddress }}</b> (hereinafter referred to as "" which expression
        shall where the context so admits, include successors-in-title and
        assigns) of the second part;
      </p>
      <br />
      <br />
      <br />
    </div>
  </div>
</template>

<script >
import { ref } from "@vue/reactivity";

import BaseInput from "../inputs/BaseInput.vue";
import BaseSelect from "../inputs/BaseSelect.vue";
import BaseRadioGroup from "../inputs/BaseRadioGroup.vue";
import BaseTextarea from "../inputs/BaseTextarea.vue"

export default {
  components: {
    BaseInput,
    BaseSelect,
    BaseRadioGroup,
    BaseTextarea
  },
  setup(props, context) {
    const entityTypes = ref([
      "Private limited liability company",
      "Public limited liability company",
    ]);

    const subscriberTypes = ref([
      { label: 'Legal Entity', value: "Legal Entity"},
      { label: 'Individual', value: "Individual"}
    ])

    const form = ref({
      subscriberType: "Legal Entity",
      entityType: null,
      entityName: "",
      regNo: "",
      regAddress: "",
      regCountry: "",
      PostShares: "",
      firstName: "",
      lastName: "",
    });

    const nextComp = () => {
      context.emit("next");
    };

    return {
      subscriberTypes,
      entityTypes,
      form,
      nextComp,
    };
  },
};
</script>

<style>
.stage {
  display: flex;
}

@media (max-width: 997px) {
  .stage {
    flex-direction: column;
  }
}

.radios {
  margin-top: 1rem;
}

.legal-entity {
  margin-right: 2rem;
}

#exampleRadios1:checked {
  background-color: black;
  border-color: white;
}

#exampleRadios2:checked {
  background-color: black;
  border-color: white;
}

.form-check-input {
  cursor: pointer;
  width: 1em !important;
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
  width: 40%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid rgb(92, 92, 92);
  font-size: 0.9rem;
  cursor: pointer;
}

@media (max-width: 997px) {
  .entity-type select {
    width: 50%;
  }
}

@media (max-width: 750px) {
  .entity-type select {
    width: 100%;
  }
}

.icon {
  font-size: 1.25rem;
}

.modal-dialog {
  max-width: 60% !important;
}

@media (max-width: 888px) {
  .modal-dialog {
    max-width: 80% !important;
  }
}

@media (max-width: 577px) {
  .modal-dialog {
    margin-left: 3rem !important;
  }
}

.modal-header {
  background-color: #002147;
  color: white;
  display: block;
}

.individual-form {
  margin-top: 1rem;
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
  width: 40%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid rgb(92, 92, 92);
  font-size: 0.9rem;
}

@media (max-width: 997px) {
  .form input {
    width: 50%;
  }
}

@media (max-width: 750px) {
  .form input {
    width: 100%;
  }
}

.form textarea {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid rgb(92, 92, 92);
  width: 75%;
}

@media (max-width: 997px) {
  .form textarea {
    width: 100%;
  }
}

.next-btn,
.next-btn {
  width: 100%;
  background: #002147;
  border-radius: 5px;
  margin-top: 1.25rem;
  padding: 10px;
  color: white;
  font-weight: 600;
  margin-bottom: 1rem;
  border: 0;
}

.next-btn:hover {
  background-color: #7e7774;
}

.next-btn:disabled,
.next-btn:disabled {
  cursor: not-allowed;
  opacity: 0.2;
}

.agreement-sheet {
  width: 40%;
  position: fixed;
  right: 5px;
  margin-top: -4rem;
  font-size: 0.8rem;
}

@media (max-width: 992px) {
  .agreement-sheet {
    position: relative;
    width: 100%;
    margin: 5rem 0;
  }
}
</style>