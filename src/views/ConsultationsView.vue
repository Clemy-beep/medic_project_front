<template>
  <div id="consult">
    <h1>Consultations</h1>
    <ConsultationsList></ConsultationsList>
  </div>
</template>

<script>
import ConsultationsList from "../components/ConsultationsList.vue";
export default {
  name: "ConsultationsView",
  components: {
    ConsultationsList,
  },
};
</script>
