<template>
  <div class="home">
    <Header />
    <div class="sub-agreement">
      <h2>Share Subscription Agreement</h2>
    </div>
    <div class="agreement">
      <AgreementInfo />
      <!-- <AgreementSheet /> -->
    </div>
  </div>
</template>

<script setup>
  import Header from "../components/Header.vue"
  import AgreementInfo from "../components/AgreementInfo.vue";
  import AgreementSheet from "../components/AgreementSheet.vue";
</script>

<style scoped>
  .home {
    /* border: 2px solid rgb(255, 251, 0); */
  }

  .sub-agreement {
    /* border: 2px solid black; */
  }

  h2 {
    /* border: 2px solid rgb(255, 0, 0); */
    font-weight: 400;
    width: 70%;
    margin: 2rem auto;
    text-align: center;
  }

  .agreement {
    /* border: 2px solid blue; */
    /* display: flex;
    justify-content: space-between; */
    width: 95%;
    float: right;
  }

  @media (max-width: 992px) {
    /* .agreement {
      flex-direction: column;
    } */
  }
</style>