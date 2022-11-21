<template>
  <div class="stage">
    <div class="w-100 border mt-4 p-2 pt-3 rounded">
      <h3>Subscription Terms</h3>
      <form @submit.prevent="" class="legal-entity-form">
        <br>
        <label>Will the subscriber be entitled to a director?*</label>
        <div class="d-flex radios" >
          <div class="form-check legal-entity">
            <input 
            @click="directorYes"
            class="form-check-input" 
            id="exampleRadios1" 
            name="exampleRadios" 
            value="yes"
            required
            type="radio" 
            >
            <label class="form-check-label" for="exampleRadios1">
              Yes
            </label>
          </div>
          <div class="form-check">
            <input 
            @click="directorNo"
            class="form-check-input"
            id="exampleRadios2" 
            name="exampleRadios" 
            value="no" 
            type="radio" 
            checked >
            <label class="form-check-label" for="exampleRadios2">
              No
            </label>
          </div>
        </div>

        <div class="form" v-if="showDirectorNo">
          <label>How many Directors will be Subscriber be entitled to?*</label>
          <input type="number" placeholder="Ex: 5" required>
        </div>
        <br>
        <label>Will there be a limit to the number of directors?*</label>
        <div class="d-flex radios">
          <div class="form-check legal-entity">
            <input 
            @click="directorLimitYes"
            class="form-check-input" 
            id="exampleRadios1" 
            name="exampleRadios2" 
            required
            value="yes"
            type="radio" >
            <label class="form-check-label" for="exampleRadios1">
              Yes
            </label>
          </div>
          <div class="form-check">
            <input 
            @click="directorLimitNo"
            class="form-check-input"
            id="exampleRadios2" 
            name="exampleRadios2" 
            value="no" 
            type="radio" 
            checked >
            <label class="form-check-label" for="exampleRadios2">
              No
            </label>
          </div>
        </div>

        <div class="form" v-if="showDirectorLimit">
          <label>What is the limit on the number of directors in the Company*</label>
          <input type="number" placeholder="Ex: 1" required>
        </div>
        <div class="form">
          <label>Insert Subscription Price*</label>
          <input type="number" placeholder="Ex: 500" v-model="subPrice" required>
        </div>
        <br>
        <label>Will the transaction include an anti-dilution clause?</label>
        <div class="d-flex radios">
          <div class="form-check legal-entity">
            <input 
            class="form-check-input" 
            id="exampleRadios1" 
            name="exampleRadios3" 
            value="yes4"
            type="radio" >
            <label class="form-check-label" for="exampleRadios1">
              Yes
            </label>
          </div>
          <div class="form-check">
            <input 
            class="form-check-input"
            id="exampleRadios2" 
            name="exampleRadios3" 
            value="no5" 
            type="radio"
            checked >
            <label class="form-check-label" for="exampleRadios2">
              No
            </label>
          </div>
        </div> 

        <button class="next-btn" :disabled="!subPrice" @click="nextComp">Next</button>
      </form>
    </div>

    <div class="agreement-sheet">
      <span class="fs-6 fw-bold">
        THIS  SHARE SHAREHOLDERS' AGREEMENT is made this ____ day of __________ 20____
      </span>
      <br> <br>
      <span class="fs-6 fw-bold">Anti-Dilution</span>
      <br> <br>
      <p>
        It is hereby agreed that the Subscriber shall at all times be protected against dilution of its shareholding in the Company
      </p>
      <p>
        If the Company issues any new shares after the Completion Date, 
        which are priced on the basis of a pre-money valuation of the Company that is lower 
        than the post-money valuation relating the investment made by the Subscriber, the Company shall, 
        unless and to the extent that the Subscriber shall have specifically waived its rights under this paragraph in writing, 
        issue to the Subscriber, at no extra cost to the Subscriber, 
        such number of shares to the extent that the Subscriber shall after such allotment hold not less than 
        13% (thirteen percent) of the Company’s share capital
      </p>
      <br> <br> <br>
    </div>
  </div>
  
</template>

<script>
  import { ref } from "vue"

  export default {
    setup (props, context) {
      const selected = ref();

      const showDirectorNo = ref(false)

      const directorYes = () => {
        showDirectorNo.value = true
      }

      const directorNo = () => {
        showDirectorNo.value = false
      }

      const showDirectorLimit = ref(false)

      const directorLimitYes = () => {
        showDirectorLimit.value = true
      }

      const directorLimitNo = () => {
        showDirectorLimit.value = false
      }

      const subPrice = ref("");

      const nextComp = () => {
        context.emit('next')
      }

      return {
        selected,
        showDirectorNo,
        directorYes,
        directorNo,
        showDirectorLimit,
        directorLimitYes,
        directorLimitNo,
        subPrice,
        nextComp
      }
    }
  }

  
</script>
