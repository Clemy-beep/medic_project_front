<template>
  <div id="patient">
    {{ patient.name }}
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "PatientComponent",
  mounted() {
    this.fetchPatient();
  },
  props: {
    id: String,
  },
  data() {
    return {
      patient: {},
    };
  },
  methods: {
    async fetchPatient() {
      this.patient = await axios
        .get(`https://apidoctor.quidam.re${this.id}/`, {
          headers: {
            Authorization: `Bearer ${sessionStorage.getItem("token")}`,
          },
        })
        .then((res) => {
          console.log(res);
          return res.data;
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>

<style scoped>
div {
  font-weight: 600;
}
</style>
