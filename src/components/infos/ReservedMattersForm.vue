<template>
  <div class="stage">
    <div class="w-100">
      <div class="border mt-4 p-2 pt-3 rounded">
        <h3>Reserved Matters</h3>
        <form @submit.prevent="" class="legal-entity-form">
          <BaseTextarea
            v-model="form.newReservedMatter"
            label="Insert new Reserved Matter"
            placeholder="Ex: File all annual returns with the CAC"
          />
          <BaseTextarea
            v-model="form.newInfo"
            label="Insert new Information Right"
            placeholder="Ex: File all annual returns with the CAC"
          />
          <button class="next-btn insert" type="submit" @click="addMatters">
            Insert Condition <i class="bi bi-forward"></i>
          </button>
        </form>
      </div>

      <div class="btns d-flex justify-content-between">
        <button class="next-btn previous" @click="previousComp">Back</button>
        <button class="next-btn forward" @click="nextComp">Next</button>
      </div>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        THIS SHARE SHAREHOLDERS' AGREEMENT is made this ____ day of __________
        20____
      </span>
      <br />
      <br />
      <!-- new Reserved Matter* -->
      <p>
        The Company and the Sponsors shall ensure that the consent of the
        Subscriber shall be first had and obtained in relation to the following
        matters, provided that such consent shall not be unreasonably withheld,
        delayed or conditioned (the “Reserved Matters”):
      </p>
      <div v-for="(matter, index) in matters" :key="index">
        <p>
          {{ index + 11.1 }} {{ matter.newReservedMatter }}
          <i class="bi bi-trash icon" @click="deleteDefinition(index)"></i>
        </p>
      </div>
      <!-- new Information Right* -->
      <p>
        The Subscriber shall be entitled to receive the following information
        and/or documents from the Company:
      </p>
      <div v-for="(matter, index) in matters" :key="index">
        <p>{{ index + 11.1 }} {{ matter.newInfo }}</p>
      </div>
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
      newReservedMatter: "",
      newInfo: "",
    });

    const nextComp = () => {
      context.emit("next");
    };

    const previousComp = () => {
      context.emit("previous");
    };

    const matters = ref([{ term: "", meaning: "" }]);

    matters.value.shift();
    const addMatters = () => {
      if ((form.value.newInfo !== "") & (form.value.newReservedMatter !== "")) {
        matters.value.push({
          newInfo: form.value.newInfo,
          newReservedMatter: form.value.newReservedMatter,
        });

        form.value.newInfo = "";
        form.value.newReservedMatter = "";
      }
    };

    const deleteDefinition = (index) => {
      matters.value.splice(index, 1);
    };

    return {
      form,
      nextComp,
      previousComp,
      matters,
      addMatters,
      deleteDefinition,
    };
  },
};
</script>

<style>
.insert:hover {
  background-color: #033772;
}

.previous {
  width: 49.7%;
  background-color: #e0e1e2;
  color: black;
}

.previous:hover {
  background-color: #cacbcd;
}

.forward {
  width: 49.7%;
}
</style>