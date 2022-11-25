<template>
  <div class="home">
    <Header />
    <div class="sub-agreement">
      <h2>Share Subscription Agreement</h2>
    </div>
    <div class="agreement">
      <AgreementInfo />
    </div>
  </div>
</template>

<script setup>
  import Header from "../components/Header.vue"
  import AgreementInfo from "../components/AgreementInfo.vue";
</script>

<style scoped>
  h2 {
    font-weight: 400;
    width: 70%;
    margin: 2rem auto;
    text-align: center;
  }

  .agreement {
    width: 95%;
    float: right;
  }
</style>