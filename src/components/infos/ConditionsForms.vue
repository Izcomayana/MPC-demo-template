<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Completion Conditions</h3>    
      <form @submit.prevent="" class="legal-entity-form">
        <div class="form">
          <form>
            <label>Add Additional Completion Condition*</label>
            <textarea 
              v-model="additionalCondition" 
              cols="10" 
              rows="5" 
              required
              placeholder="Ex: File all annual returns with the CAC">
            </textarea>
          </form>
          <button class="next-btn" type="submit" @click="addCondition">Insert Condition <i class="bi bi-forward"></i></button>
        </div>
        
        <button class="next-btn" :disabled="!additionalCondition" @click="nextComp">Next</button>
      </form>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        2. COMPLETION CONDITIONS
      </span>
      <br> <br>
      <p>
        2.1 The provision of Completion conditional clauses 
        are on the following having occurred on or before 5.00pm (GMT) on the Long Stop Date:
      </p>

      <div class="card">
        <ul class="list-group list-group-flush">
          <li class="list-group-item"  v-for="(condition, index) in conditions" :key="index">
            {{ 1.1 + index }} {{ condition.condition }} 
            <i class="bi bi-trash icon"  @click="deleteCondition(index)"></i>
            <i 
              class="bi bi-pencil-fill icon"
              data-bs-toggle="modal" 
              data-bs-target="#exampleModal"
              @click="editCondition(condition)">
            </i>

            <!-- <div v-if="condition === conditionToEdit" class="modal fade" id="exampleModal" >
              <input type="text" v-model="condition.condition" >
              <button @click="saveCondition(condition.id)">Save</button>
              <button @click="cancleEditMode">Cancle</button>
            </div> -->
            <div>
              <div class="modal fade" id="exampleModal"  aria-labelledby="exampleModalLabel" aria-hidden="true" v-if="condition == conditionToEdit">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h5 class="modal-title" id="exampleModalLabel">Adjust Conditions</h5>
                      <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                      <form>
                        <div class="mb-3">
                          <textarea class="form-control" id="message-text" v-model="condition.condition"></textarea>
                        </div>
                      </form>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                      <button type="button" class="btn btn-primary">Save Changes</button>
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
  import { ref } from "vue"

  export default {
    setup (props, context) {
      const additionalCondition = ref("");

      const addCondition = () => {
        if (additionalCondition.value !== "") {
          conditions.value.push({
            condition: additionalCondition.value
          });
        }
      }

      const nextComp = () => {
        context.emit('next')
      }
      
      const conditions = ref([
        {
          condition: "execution of the Transaction Documents "
        },
        {
          condition: "waivers duly executed by the existing shareholders of the Company waiving any and all pre-emptive rights or right of first offer or refusal in respect of the Subscription Shares under the CAMA or otherwise"
        },
        {
          condition: "no event having a Material Adverse Effect has occurred",
        }
      ]);

      const deleteCondition = (index) => {
        conditions.value.splice(index, 1);
      }

      const conditionToEdit = ref()

      const editCondition = (condition) => {
        conditionToEdit.value = condition
      }

      const saveCondition = async (postId) => {
        conditionToEdit.value = (false)
      }

      const cancleEditMode = () => {
        conditionToEdit.value = (false)
      }

      return {
        additionalCondition,
        addCondition,
        nextComp,
        conditions,
        deleteCondition,
        conditionToEdit,
        editCondition,
        saveCondition,
        cancleEditMode
      }
    }
  }
</script>

<style>
  .agreement-sheet {
    position: absolute;
  }

  @media (max-width: 992px) {
    .agreement-sheet {
      position: relative;
    }
  }
</style>