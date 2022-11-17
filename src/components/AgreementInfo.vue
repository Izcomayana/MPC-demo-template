<template>
  <div class="agreement-info">
    <div class="info-con rounded shadow">
      <div class="info">
        <!-- <h5>Subscriber</h5> -->
        <p @click="subscriber">1</p>
      </div>

      <div class="info">
        <!-- <h5>Sponsor(s) Info</h5> -->
        <p @click="sponsor">2</p>
      </div>
      
      <div class="info">
        <!-- <h5>Target Company Information</h5> -->
        <p @click="targetCompany">3</p>
      </div>
      <div class="info">
        <!-- <h5>Subscription Price</h5> -->
        <p @click="subPrice">4</p>
      </div>
      <div class="info">
        <!-- <h5>Subscription Terms</h5> -->
        <p @click="subTerms">5</p>
      </div>
      <div class="info">
        <!-- <h5>Completion Conditions</h5> -->
        <p @click="conditions">6</p>
      </div>
      <div class="info">
        <!-- <h5>Reserved Matters</h5> -->
        <p @click="reservedMatters">7</p>
      </div>
      <div class="info">
        <!-- <h5>Shareholding</h5> -->
        <p @click="shareholders">8</p>
      </div>
      <div class="info">
        <!-- <h5>Definitions</h5> -->
        <p @click="definitions">9</p>
      </div>
      <div class="info">
        <!-- <h5>Disclosures</h5> -->
        <p @click="disclosures">10</p>
      </div>
    </div>

    <div class="info-forms">
      <div v-if="showSubscriber">
        <SubscriberForm @next="sponsor" />
      </div>
      <div v-if="showSponsor">
        <SponsorForm  @next="targetCompany" />
      </div>
      <div v-if="showTargetCompany">
        <TLCForm  @next="subPrice" />
      </div>
      <div v-if="showSubPrice">
        <SubPriceForm  @next="subTerms" />
      </div>
      <div v-if="showSubTerms">
        <SubTermsForm  @next="conditions" />
      </div>
      <div v-if="showConditions">
        <ConditionsForm  @next="reservedMatters" />
      </div>
      <div v-if="showReservedMatters">
        <ReservedMattersForm  @next="shareholders" />
      </div>
      <div v-if="showShareholders">
        <ShareHoldersForm  @next="definitions" />
      </div>
      <div v-if="showDefinitions">
        <DefinitionsForm  @next="disclosures" />
      </div>
      <div v-if="showDisclosures">
        <DisclosedAgreementForm  @next="disclosures" />
      </div>
    </div>
  </div>
</template>

<script>
  import { ref } from "vue";

  // components
  import SubscriberForm from "./infos/SubscriberForm.vue";
  import SponsorForm from "./infos/SponsorForm.vue";
  import TLCForm from "./infos/TCIForm.vue"
  import SubPriceForm from "./infos/SubPriceForm.vue"
  import SubTermsForm from "./infos/SubTerms.vue";
  import ConditionsForm from "./infos/ConditionsForms.vue"
  import ReservedMattersForm from "./infos/ReservedMattersForm.vue"
  import ShareHoldersForm from "./infos/ShareholdersForm.vue"
  import DefinitionsForm from "./infos/DefinitionsForm.vue"
  import DisclosedAgreementForm from "./infos/DisclosedAgreementForm.vue"

  export default {
    components: {
      SubscriberForm,
      SponsorForm,
      TLCForm,
      SubPriceForm,
      SubTermsForm,
      ConditionsForm,
      ReservedMattersForm,
      ShareHoldersForm,
      DefinitionsForm,
      DisclosedAgreementForm
    },
    setup () {
      const showSubscriber = ref(true);
      const showSponsor = ref(false);
      const showTargetCompany = ref(false);
      const showSubPrice = ref(false);
      const showSubTerms = ref(false);
      const showDefinitions = ref(false);
      const showReservedMatters = ref(false);
      const showShareholders = ref(false);
      const showConditions = ref(false);
      const showDisclosures = ref(false);


      const subscriber = () => {
        showSubscriber.value = true;
        showSponsor.value = false;
        showTargetCompany.value = false;
        showSubPrice.value = false;
        showSubTerms.value = false;
        showDefinitions.value = false;
        showReservedMatters.value = false;
        showShareholders.value = false;
        showConditions.value = false;
        showDisclosures.value = false;
      }

      const sponsor = () => {
        showSubscriber.value = false;
        showSponsor.value = true;
        showTargetCompany.value = false;
        showSubPrice.value = false;
        showSubTerms.value = false;
        showDefinitions.value = false;
        showReservedMatters.value = false;
        showShareholders.value = false;
        showConditions.value = false;
        showDisclosures.value = false;
      }

      const targetCompany = () => {
        showSubscriber.value = false;
        showSponsor.value = false;
        showTargetCompany.value = true;
        showSubPrice.value = false;
        showSubTerms.value = false;
        showDefinitions.value = false;
        showReservedMatters.value = false;
        showShareholders.value = false;
        showConditions.value = false;
        showDisclosures.value = false;
      }

      const subPrice = () => {
        showSubscriber.value = false;
        showSponsor.value = false;
        showTargetCompany.value = false;
        showSubPrice.value = true;
        showSubTerms.value = false;
        showDefinitions.value = false;
        showReservedMatters.value = false;
        showShareholders.value = false;
        showConditions.value = false;
        showDisclosures.value = false;
      }

      const subTerms = () => {
        showSubscriber.value = false;
        showSponsor.value = false;
        showTargetCompany.value = false;
        showSubPrice.value = false;
        showSubTerms.value = true;
        showDefinitions.value = false;
        showReservedMatters.value = false;
        showShareholders.value = false;
        showConditions.value = false;
        showDisclosures.value = false;
      }

      const conditions = () => {
        showSubscriber.value = false;
        showSponsor.value = false;
        showTargetCompany.value = false;
        showSubPrice.value = false;
        showSubTerms.value = false;
        showDefinitions.value = false;
        showReservedMatters.value = false;
        showShareholders.value = false;
        showConditions.value = true;
        showDisclosures.value = false;
      }
      
      const reservedMatters = () => {
        showSubscriber.value = false;
        showSponsor.value = false;
        showTargetCompany.value = false;
        showSubPrice.value = false;
        showSubTerms.value = false;
        showDefinitions.value = false;
        showReservedMatters.value = true;
        showShareholders.value = false;
        showConditions.value = false;
        showDisclosures.value = false;
      }

      const shareholders = () => {
        showSubscriber.value = false;
        showSponsor.value = false;
        showTargetCompany.value = false;
        showSubPrice.value = false;
        showSubTerms.value = false;
        showDefinitions.value = false;
        showReservedMatters.value = false;
        showShareholders.value = true;
        showConditions.value = false;
        showDisclosures.value = false;
      }

      const definitions = () => {
        showSubscriber.value = false;
        showSponsor.value = false;
        showTargetCompany.value = false;
        showSubPrice.value = false;
        showSubTerms.value = false;
        showDefinitions.value = true;
        showReservedMatters.value = false;
        showShareholders.value = false;
        showConditions.value = false;
        showDisclosures.value = false;
      }

      const disclosures = () => {
        showSubscriber.value = false;
        showSponsor.value = false;
        showTargetCompany.value = false;
        showSubPrice.value = false;
        showSubTerms.value = false;
        showDefinitions.value = false;
        showReservedMatters.value = false;
        showShareholders.value = false;
        showConditions.value = false;
        showDisclosures.value = true;
      }

      return {
        showSubscriber,
        showSponsor,
        showTargetCompany,
        showSubPrice,
        showSubTerms,
        showDefinitions,
        showReservedMatters,
        showShareholders,
        showConditions,
        showDisclosures,
        subscriber,
        sponsor,
        targetCompany,
        subPrice,
        subPrice,
        subTerms,
        definitions,
        reservedMatters,
        shareholders,
        conditions,
        disclosures,
      }
    }
  }


  
  
</script>

<style>
  .agreement-info {
    /* border: 2px solid black; */
    width: 55%;
    font-size: 0.9rem;
  }

  @media (max-width: 992px) {
    .agreement-info {
      width: 92%;
      margin-bottom: 5rem;
    }
  }

  .info-con {
    /* border: 0.5px solid rgb(185, 185, 185); */
    border-radius: 7.5px;
    justify-content: space-between;
    align-items: center;
    display: flex;
    padding: 0.75rem;
  }

  .info {
    width: 7.5%;
    text-align: center;
    font-size: 0.8rem;
    font-weight: 400;
  }

  .info h5 {
    font-size: 0.8rem;
    font-weight: 400;
  }

  /* .info h5 {
    font-size: 0.9rem;
    font-weight: 400;
    margin-top: 0;
    margin-bottom:1.1rem;
  } */

  .info p {
    background: #eeeeee;
    border-radius: 1rem;
    color: gray;
    cursor: pointer;
    font-size: 1.3rem;
    margin: 0 auto;
    margin-bottom: 0;
    /* margin-top: 0.5rem; */
    width: 2rem;
  }

  @media (max-width: 750px) {
    .info p {
      font-size: 0.75rem;
      width: 1.3rem;
    }
  }

  .info p:active,
  .info p:focus {
    background: #002147;
  }
</style>