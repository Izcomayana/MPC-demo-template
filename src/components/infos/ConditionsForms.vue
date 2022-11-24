<template>
  <div class="stage">
    <div class="w-100">
      <div class="border mt-4 p-2 pt-3 rounded">
        <h3>Completion Conditions</h3>
        <form @submit.prevent="" class="legal-entity-form">
          <div class="form">
            <form>
              <BaseTextarea
                v-model="form.additionalCondition"
                label="Add Additional Completion Condition"
                placeholder="Ex: File all annual returns with the CAC"
              />
            </form>
            <button class="next-btn insert" type="submit" @click="addCondition">
              Insert Condition <i class="bi bi-forward"></i>
            </button>
          </div>
        </form>
      </div>

      <div class="btns d-flex justify-content-between">
        <button class="next-btn previous" @click="previousComp">Back</button>
        <button class="next-btn forward" @click="nextComp">Next</button>
      </div>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold"> 6. COMPLETION CONDITIONS </span>
      <br />
      <br />
      <p>
        Following the Completion Date, but no later than the Longstop Date, the
        Company & the Sponsors shall procure the following:
      </p>

      <div class="card">
        <ul class="list-group list-group-flush">
          <li
            class="list-group-item"
            v-for="(condition, index) in conditions"
            :key="index"
          >
            {{ 1.1 + index }} {{ condition.condition }}
            <i class="bi bi-trash icon" @click="deleteCondition(index)"></i>
            <i
              class="bi bi-pencil-fill icon"
              data-bs-toggle="modal"
              data-bs-target="#exampleModal"
              @click="editCondition(condition)"
            >
            </i>
            <div>
              <div
                class="modal fade"
                id="exampleModal"
                aria-labelledby="exampleModalLabel"
                aria-hidden="true"
                v-if="condition == conditionToEdit"
              >
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h5 class="modal-title" id="exampleModalLabel">
                        Adjust Conditions
                      </h5>
                      <button
                        type="button"
                        class="btn-close"
                        data-bs-dismiss="modal"
                        aria-label="Close"
                      ></button>
                    </div>
                    <div class="modal-body">
                      <form>
                        <div class="mb-3">
                          <textarea
                            class="form-control"
                            id="message-text"
                            v-model="condition.condition"
                          ></textarea>
                        </div>
                      </form>
                    </div>
                    <div class="modal-footer">
                      <button
                        type="button"
                        class="btn btn-secondary"
                        data-bs-dismiss="modal"
                      >
                        Close
                      </button>
                      <button type="button" class="btn btn-primary">
                        Save Changes
                      </button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

import BaseTextarea from "../inputs/BaseTextarea.vue";

export default {
  components: {
    BaseTextarea
  },
  setup(props, context) {
    const form = ref({
      additionalCondition: ""
    })

    const addCondition = () => {
      if (form.value.additionalCondition !== "") {
        conditions.value.push({
          condition: form.value.additionalCondition,
        });
      }
      form.value.additionalCondition = "";
    };

    const nextComp = () => {
      context.emit("next");
    };

    const previousComp = () => {
      context.emit("previous");
    };

    const conditions = ref([]);

    const deleteCondition = (index) => {
      conditions.value.splice(index, 1);
    };

    const conditionToEdit = ref();

    const editCondition = (condition) => {
      conditionToEdit.value = condition;
    };

    const saveCondition = async (postId) => {
      conditionToEdit.value = false;
    };

    const cancleEditMode = () => {
      conditionToEdit.value = false;
    };

    return {
      form,
      addCondition,
      nextComp,
      previousComp,
      conditions,
      deleteCondition,
      conditionToEdit,
      editCondition,
      saveCondition,
      cancleEditMode,
    };
  },
};
</script>

<style scoped>
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

.agreement-sheet {
  position: absolute;
}

@media (max-width: 992px) {
  .agreement-sheet {
    position: relative;
  }
}
</style>