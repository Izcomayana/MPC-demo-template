<template>
  <div class="stage">
    <div class="w-100">
      <div class="border mt-4 p-2 pt-3 rounded">
        <h3>Definitions</h3>
        <form @submit.prevent="" class="legal-entity-form">
          <BaseInput
            v-model="form.term"
            label="Defined Term"
            type="text"
            placeholder="Ex: Oluwapelumi Sotoyinbo"
          />
          <BaseTextarea
            v-model="form.meaning"
            label="Meaning"
          />
          <button class="next-btn" type="submit" @click="addDefinition">
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
      <span class="fs-6 fw-bold"> 1 DEFINITIONS AND INTERPRETATION </span>
      <br />
      <br />
      <p>
        Unless the context otherwise requires, in this Agreement, the Recitals
        and Schedules hereto, the following expressions shall have the meanings
        respectively assigned to them:
      </p>
      <!-- On tables -->
      <div>
        <table class="table table-hover table-bordered">
          <thead class="table-light">
            <tr>
              <th scope="col">Term</th>
              <th scope="col">Meaning</th>
            </tr>
          </thead>
          <tbody v-if="showTable">
            <tr v-for="(definition, index) in definitions" :key="index">
              <td>
                {{ definition.term }}
                <i
                  class="bi bi-trash icon"
                  @click="deleteDefinition(index)"
                ></i>
              </td>
              <td>{{ definition.meaning }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <br />
      <br />
      <br />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

import BaseInput from "../inputs/BaseInput.vue";
import BaseTextarea from "../inputs/BaseTextarea.vue";

export default {
  components: {
    BaseInput,
    BaseTextarea
  },
  setup(props, context) {
    const form = ref({
      term: "",
      meaning: ""
    })
    
    const nextComp = () => {
      context.emit("next");
    };

    const previousComp = () => {
      context.emit("previous");
    };

    const definitions = ref([{ term: "", meaning: "" }]);

    const showTable = ref(false);

    definitions.value.shift();
    const addDefinition = () => {
      if ((form.value.term !== "") & (form.value.meaning !== "")) {
        showTable.value = true;
        definitions.value.push({
          term: form.value.term,
          meaning: form.value.meaning,
        });

        form.value.term = "";
        form.value.meaning = "";
      }
    };

    const deleteDefinition = (index) => {
      definitions.value.splice(index, 1);
    };

    return {
      form,
      nextComp,
      previousComp,
      definitions,
      showTable,
      addDefinition,
      deleteDefinition,
    };
  },
};
</script>
