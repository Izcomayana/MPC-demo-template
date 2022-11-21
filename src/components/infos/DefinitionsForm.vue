<template>
  <div class="stage">
    <div class="w-100">
      <div class="border mt-4 p-2 pt-3 rounded">
        <h3>Definitions</h3>    
        <form @submit.prevent="" class="legal-entity-form">
          <div class="form">
            <label>Defined Term*</label>
            <input v-model="term" type="text" placeholder="Ex: Oluwapelumi Sotoyinbo" required>
          </div>
          <div class="form">
            <label>Meaning*</label>
            <textarea v-model="meaning" cols="10" rows="5" required></textarea>
          </div>
          <button class="next-btn" type="submit" @click="addDefinition">Insert Condition <i class="bi bi-forward"></i></button>
        </form>
      </div>

      <div class="btns d-flex justify-content-between">
        <button class="next-btn previous" @click="previousComp">Back</button>
        <button class="next-btn forward" @click="nextComp">Next</button>
      </div>
    </div>
    
    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        1 DEFINITIONS AND INTERPRETATION
      </span>
      <br> <br>
      <p>
        Unless the context otherwise requires, in this Agreement, 
        the Recitals and Schedules hereto, the following expressions 
        shall have the meanings respectively assigned to them:
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
              <td>{{ definition.term }} <i class="bi bi-trash icon"  @click="deleteDefinition(index)"></i></td>
              <td>{{ definition.meaning }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <br> <br> <br>
    </div>
  </div>
</template>

<script>
  import { ref } from "vue";

  export default {
    setup (props, context) {
      const term = ref("");
      const meaning = ref("");

      const nextComp = () => {
        context.emit('next')
      }

      const previousComp = () => {
        context.emit('previous');
      }

      const definitions = ref([
        { term: "", meaning: "" }
      ]);

      const showTable = ref(false);

      definitions.value.shift()
      const addDefinition = () => {
        if (term.value !== "" & meaning.value !== "") {
          showTable.value = true
          definitions.value.push({
            term: term.value,
            meaning: meaning.value,
          });

          term.value = ""
          meaning.value = ""
        }
      }

      const deleteDefinition = (index) => {
        definitions.value.splice(index, 1);
      }

      return {
        term,
        meaning,
        nextComp,
        previousComp,
        definitions,
        showTable,
        addDefinition,
        deleteDefinition
      }
    }
  }
</script>
