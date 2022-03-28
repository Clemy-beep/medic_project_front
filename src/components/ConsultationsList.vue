<template>
  <div id="consult-list">
    <ul v-for="consultation in consultations" :key="consultation.id">
      <li>
        Apointment date: {{ consultation.date }} with patient
        <PatientComponent v-bind:id="consultation.patient"></PatientComponent>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import PatientComponent from "../components/PatientComponent.vue";
export default {
  components: {
    PatientComponent,
  },
  mounted() {
    this.fetchConsultations();
  },
  name: "ConsultationsList",
  data() {
    return {
      consultations: [],
    };
  },
  methods: {
    async fetchConsultations() {
      console.log("Fetching");
      this.consultations = await axios
        .get("https://apidoctor.quidam.re/api/consultations/", {
          headers: {
            Authorization: `Bearer ${sessionStorage.getItem("token")}`,
          },
        })
        .then((res) => {
          console.log(res);
          if (res.code === 401 && res.message === "Expired JWT Token")
            this.$router.push("/");
          return res.data["hydra:member"];
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>
