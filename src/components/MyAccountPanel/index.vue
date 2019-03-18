<template>
  <div class="s1-loc__my-account-panel">
    <account-button/>
    <!-- <div class="s1-U__pd8"></div>
    <apps-button/>-->
  </div>
</template>

<script>
import AccountButton from "./AccountButton.vue";

export default {
  name: "MyAccountPanel",
  components: {
    AccountButton
  }
};
</script>