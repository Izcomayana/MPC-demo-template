<template>
  <div class="stage">
    <div class="w-100">
      <div class="border mt-4 p-2 pt-3 rounded">
        <h3>Shareholders</h3>
        <form @submit.prevent="" class="legal-entity-form">
          <BaseInput
            v-model="form.name"
            label="Name"
            type="text"
            placeholder="Ex: Oluwapelumi Sotoyinbo"
          />
          <BaseTextarea
            v-model="form.address"
            label="Address"
            placeholder="Ex: 123 West End Lane Ikota"
          />
          <BaseInput
            v-model="form.shareholding"
            label="Shareholding%"
            type="number"
            placeholder="Ex: 40"
          />

          <button class="next-btn" type="submit" @click="addShareholder">
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
        SCHEDULE 2 <br />
        A. EXISTING SHAREHOLDERS AND SHAREHOLDING
      </span>
      <br />
      <br />
      <!-- On tables -->
      <div>
        <table class="table table-hover table-bordered">
          <thead class="table-light">
            <tr>
              <th scope="col">Name of Shareholder</th>
              <th scope="col">Address of Shareholder</th>
              <th scope="col">% of Issued Shares</th>
            </tr>
          </thead>
          <tbody v-if="showTable">
            <tr v-for="(shareholder, index) in shareholders" :key="index">
              <td>
                {{ shareholder.name }}
                <i
                  class="bi bi-trash icon"
                  @click="deleteShareholder(index)"
                ></i>
              </td>
              <td>{{ shareholder.address }}</td>
              <td>{{ shareholder.percent }}</td>
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
import { reactive, ref } from "vue";

import BaseInput from "../inputs/BaseInput.vue";
import BaseTextarea from "../inputs/BaseTextarea.vue";

export default {
  components: {
    BaseInput,
    BaseTextarea
  },
  setup(props, context) {
    const form = reactive({
      name: "",
      address: "",
      shareholding: ""
    })

    const shareholders = ref([{ name: "", address: "", percent: "" }]);

    const nextComp = () => {
      context.emit("next");
    };

    const previousComp = () => {
      context.emit("previous");
    };

    const showTable = ref(false);

    shareholders.value.shift();

    const addShareholder = async () => {
      if (
        (form.name !== "") &
        (form.address !== "") &
        (form.shareholding !== "")
      ) {
        showTable.value = true;
        shareholders.value.push({
          name: form.name,
          address: form.address,
          percent: form.shareholding,
        });

        form.name = "";
        form.address = "";
        form.shareholding = "";
      }
    };

    const deleteShareholder = (index) => {
      shareholders.value.splice(index, 1);
    };

    return {
      form,
      context,
      shareholders,
      showTable,
      addShareholder,
      nextComp,
      previousComp,
      deleteShareholder
    };
  },
};
</script>
