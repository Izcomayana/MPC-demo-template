<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-3 pt-3 rounded">
      <h3>Details of the subscriber</h3>
      <br>
      <div class="d-flex radios">
        <div class="form-check legal-entity">
          <input 
          @click="legalEntity"
          v-model="subscriberType"
          class="form-check-input" 
          id="exampleRadios1"
          name="subscriberType" 
          value="Legal Entity"
          type="radio" >
          <label class="form-check-label" for="exampleRadios1">
            Legal Entity
          </label>
        </div>
        <div class="form-check">
          <input 
          @click="individual"
          v-model="subscriberType"
          class="form-check-input"
          id="exampleRadios2" 
          name="subscriberType" 
          value="Individual" 
          type="radio" >
          <label class="form-check-label" for="exampleRadios2">
            Individual
          </label>
        </div>
      </div>
      
      <form @submit.prevent="" class="legal-entity-form" v-if="showlegalEntityForm">
        <div class="entity-type">
          <label for="Entity Type">Entity Type*</label>
          <select name="Entity Type" v-model="entityType" required>
            <option value="Private limited liability company">Private limited liability company</option>
            <option value="Public limited liability company">Public limited liability company</option>
          </select>
        </div>
        <div class="form">
          <label>Entity Name* 
            <i class="bi bi-info-circle-fill icon" data-bs-toggle="modal" data-bs-target="#exampleModal"></i>
          </label>
          <input type="text" v-model="entityName" placeholder="Ex: My Pocket Counsel" required>
        </div>

        <!-- Modal -->
        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
          <div class="modal-dialog">
            <div class="modal-content">
              <div class="modal-header">
                <h1 class="modal-title fs-5" id="exampleModalLabel">Drafting Note</h1>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
              </div>
              <div class="modal-body">
                <p>
                  The Company and the Sponsors will typically raise the argument that the agreement is primarily between the Company who is issuing the shares and Investor who is subscribing for the shares, hence, there is no need for the Sponsors to be a party to the Agreement. 
                  Furthermore, that based on the principle of separate corporate personality pursuant to Section 42 of the CAMA they should not be made a party or be liable under the Agreement. The Investor can rebut this position on several grounds. 
                  Firstly, that while the Company is a separate entity it is an artificial person that acts through natural persons like the Sponsors who are in charge of the daily operations and policies of the Company. 
                  Secondly, in the event of a warranty breach and the Investor makes a claim for breach of warranties such a claim is equal to the Investor receiving its invested funds without the projected returns on investment.
                </p>
                <br> <br>
                <p>
                  Thirdly, the investment is most times predicated on business plans prepared by the Sponsors and the Investor is relying on the Sponsors for implementation based on the representations and assurances giving by the Sponsors. 
                  As such, the Investor is asking the Sponsor to put their money where their mouth is. Ultimately, the negotiations depends on the bargaining strength of the parties. Where the Sponsor is made a party to the Agreement, 
                  the Sponsor can rely on several risk mitigating mechanisms discussed below.
                </p>
              </div>
              <div class="modal-footer">
                <button type="button" class="btn btn-secondary next-btn" data-bs-dismiss="modal">Close</button>
              </div>
            </div>
          </div>
        </div>

        <div class="form">
          <label>Registration Number*</label>
          <input type="number" v-model="regNo" placeholder="Ex: RC 1234">
        </div>
        <div class="form">
          <label>Registration Address*</label>
          <textarea 
          cols="10" 
          rows="5" 
          placeholder="Ex: 123 West End Lane Ikota" 
          required
          v-model="regAddress"
          ></textarea>
        </div>
        <div class="form">
          <label>Registration Country*</label>
          <input type="text" v-model="regCountry" placeholder="Ex: Nigeria" required>
        </div>
        <div class="form">
          <label>Post Completion Shares*</label>
          <input type="number" v-model="PostShares"  placeholder="0" required>
        </div>

        <button :disabled="!entityName || !regNo || !regAddress || !regCountry || !PostShares" @click="nextComp" class="next-btn">Next</button>
      </form>

      <form @submit.prevent="" class="individual-form" v-if="showIndividualForm">
        <div class="entity-name form">
          <label>First Name*</label>
          <input type="text" v-model="firstName" placeholder="Ex: Israel" required>
        </div>
        <div class="reg-no form">
          <label>Last Name*</label>
          <input type="text" v-model="lastName" placeholder="Ex: Oluwapelumi" required>
        </div>
        <div class="reg-address form">
          <label>Address*</label>
          <textarea cols="10" rows="5" v-model="regAddress" placeholder="Ex: 123 West End Lane Ikota" required></textarea>
        </div>
        <div class="post-completion form">
          <label>Post Completion Shares*</label>
          <input type="number" placeholder="0" v-model="PostShares" required>
        </div>

        <button :disabled="!firstName || !lastName || !PostShares" @click="nextComp" class="next-btn">Next</button>
      </form>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        THIS SHAREHOLDERS' AGREEMENT is made this ____ day of __________ 20____
      </span>
      <br> <br>
      <span class="fs-6 fw-bold">BY AND AMONG</span>
      <br> <br>
      <p v-if="showlegalEntityForm">
        <b>{{ entityName }}</b>, a <b>{{ entityType }}</b>, incorporated under the laws of <b>{{ regCountry }}</b> with RC Number <b>{{ regNo }}</b> having its registered address at 
        <b>{{ regAddress }}</b> (hereinafter referred to as the “Company” which expression shall where the context so permits include its successors-in-title and assigns) 
        of the first part;
      </p>
      <p v-if="showIndividualForm">
        <b>{{ firstName }}</b> <b>{{ lastName }}</b> of <b>{{ regAddress }}</b> (hereinafter referred to as "" which expression shall where the context so admits, 
        include successors-in-title and assigns) of the second part;
      </p>
      
      <span class="fs-6 fw-bold">AND</span>
      <br> <br>
      
      <span class="sponsor">
        <p>
          <b>{{ companyName }}</b>, a <b>{{ companyType }}</b> company, incorporated under the laws of Nigeria with RC Number <b>{{ regNo }}</b> having its registered address at 
          <b>{{ address }}</b> currently based in <b>{{ regCountry }}</b> (hereinafter referred to as the “Company” which expression shall where the context 
          so permits include its successors-in-title and assigns) of the second part;
        </p> 
      </span>
      <br> <br> <br>
    </div>
  </div>
</template>

<script >
  import { ref } from "@vue/reactivity";

  export default {
    setup (props, context) {
      const showlegalEntityForm = ref(true);
      const showIndividualForm = ref(false);

      const nextComp = () => {
        context.emit('next')
      }

      const legalEntity = () => {
        showlegalEntityForm.value = true;
        showIndividualForm.value = false;
      }

      const individual = () => {
        showlegalEntityForm.value = false;
        showIndividualForm.value = true;
      }

      const subscriberType = ref(null);

      const entityType = ref(null);
      const entityName = ref("");
      const regNo = ref("");
      const regAddress = ref("");
      const regCountry = ref("");
      const PostShares = ref("");

      const firstName = ref("");
      const lastName = ref("");


      return {
        nextComp,
        showlegalEntityForm,
        showIndividualForm,
        legalEntity,
        individual,
        subscriberType,
        entityType,
        entityName,
        regNo,
        regAddress,
        regCountry,
        PostShares,
        firstName,
        lastName,
        PostShares
      }
    }
  }
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
  }

  .next-btn:disabled,
  .next-btn:disabled {
    cursor: not-allowed;
    opacity: 0.2;
  }

  .agreement-sheet {
    /* border: 2px solid red; */
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