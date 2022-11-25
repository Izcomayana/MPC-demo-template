<template>
  <div class="stage">
    <div class="w-100">
      <div class="border mt-4 p-2 pt-3 rounded">
        <h3>Disclosed Agreement</h3>
        <form @submit.prevent="" class="legal-entity-form">
          <BaseTextarea
            v-model="form.agreementDescription"
            label="Agreement description"
          />
          <button class="next-btn" type="submit" @click="addDisclosure">
            Insert Condition <i class="bi bi-forward"></i>
          </button>
        </form>
      </div>

      <div class="btns d-flex justify-content-between">
        <button class="next-btn previous" @click="previousComp">Back</button>
        <button
          class="next-btn forward"
          @click="nextComp"
          data-bs-toggle="modal"
          data-bs-target="#staticBackdrop"
        >
          Review & Submit
        </button>
      </div>
    </div>

    <div class="modal-con">
      <!-- Modal -->
      <div
        class="modal fade"
        id="staticBackdrop"
        data-bs-backdrop="static"
        data-bs-keyboard="false"
        tabindex="-1"
        aria-labelledby="staticBackdropLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog modal-dialog-centered">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="staticBackdropLabel">
                Share Subscription Agreement Contract
              </h5>
              <button
                type="button"
                class="btn-close"
                data-bs-dismiss="modal"
                aria-label="Close"
              ></button>
            </div>
            <div class="modal-body">
              Your contract has been submitted successfully. We'd get back to
              you soon.
            </div>
            <div class="modal-footer">
              <button
                type="button"
                class="btn btn-secondary"
                data-bs-dismiss="modal"
              >
                Close
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold"> Schedule 4 </span>
      <br />
      <br />
      <p>Disclosed Agreements:</p>
      <div v-for="(disclosure, index) in disclosures" :key="index">
        <p>{{ index + 11.1 }} {{ disclosure.description }}</p>
      </div>
      <br />
      <br />
      <br />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

import BaseTextarea from "../inputs/BaseTextarea.vue";

export default {
  components: {
    BaseTextarea,
  },
  setup(props, context) {
    const form = ref({
      agreementDescription: "",
    });

    const nextComp = () => {
      context.emit("next");
    };

    const previousComp = () => {
      context.emit("previous");
    };

    const disclosures = ref([]);

    const addDisclosure = () => {
      if (form.value.agreementDescription !== "") {
        disclosures.value.push({
          description: form.value.agreementDescription,
        });
      }
      form.value.agreementDescription = "";
    };

    return {
      form,
      nextComp,
      previousComp,
      disclosures,
      addDisclosure,
    };
  },
};
</script>
