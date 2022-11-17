<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Shareholders</h3>    
      <form @submit.prevent="" class="legal-entity-form">
        <div class="form">
          <label>Name*</label>
          <input v-model="name" type="text" placeholder="Ex: Oluwapelumi Sotoyinbo" >
        </div>
        <div class="form">
          <label>Address</label>
          <textarea v-model="address" cols="10" rows="5" placeholder="Ex: 123 West End Lane Ikota" ></textarea>
        </div>
        <div class="form">
          <label>Shareholding%*</label>
          <input v-model="shareholding" type="number" >
        </div>

        <button class="next-btn" type="submit" @click="addShareholder">Insert Condition <i class="bi bi-forward"></i></button>
      </form>
        <button 
        class="next-btn"
        :disabled="!name || !address || !shareholding" 
        @click="nextComp">Next</button>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        SCHEDULE 2 <br>
        A. EXISTING SHAREHOLDERS AND SHAREHOLDING
      </span>
      <br> <br>
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
              <td>{{ shareholder.name }} <i class="bi bi-trash icon"  @click="deleteShareholder(index)"></i></td>
              <td>{{ shareholder.address }}</td>
              <td>{{ shareholder.percent }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <br> <br> <br>
    </div>
  </div>
</template>

<script>
  import { ref } from "vue"

  export default {
    setup (props, context) {
      const name = ref("");
      const address = ref("");
      const shareholding = ref("");

      const shareholders = ref([
        { name: "", address: "", percent: "" }
      ]);

      const nextComp = () => {
        context.emit('next')
      }

      const showTable = ref(false);

      shareholders.value.shift()
      const addShareholder = () => {
        if (name.value !== "" & address.value !== "" & shareholding.value !== "") {
          showTable.value = true
          shareholders.value.push({
            name: name.value,
            address: address.value,
            percent: shareholding.value
          });

          name.value = ""
          address.value = ""
          shareholding.value = ""
        }
      }

      const deleteShareholder = (index) => {
        shareholders.value.splice(index, 1);
      }

      return {
        name,
        address,
        shareholding,
        context,
        shareholders,
        showTable,
        addShareholder,
        nextComp,
        deleteShareholder
      }
    }
  }
</script>
