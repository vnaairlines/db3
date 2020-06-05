<template>
   
  <div v-if="currentTutorial.eticketno">
      <h3>Your E-Ticket has been created</h3>
      <h4>The id is: {{ currentTutorial.id  }}</h4>
      <h4>The e-ticket number is: {{ currentTutorial.eticketno }}</h4>
  </div>
  <div v-else>
      <h3>Sorry, there is no e-ticket in the system</h3>
      <h4>The id is: {{ currentTutorial.id  }}</h4>
  </div>
</template>

<script>
import TutorialDataService from "../services/TutorialDataService";

export default {
  name: "eticket",
  data() {
    return {
      currentTutorial: {
        id: "",
        title: "",
        description: "",
        published: false,
        trainno: "",
        fromcity: "",
        tocity: "",
        eticketno: ""
      },
      message: ""
    };
  },

  methods: {
    getTutorialdata(id) {
      TutorialDataService.get(id)
        .then(response => {
          this.currentTutorial = response.data;
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    }
  },
  mounted() {
    this.message = "";
    this.getTutorialdata(this.$route.params.id);
  }
};
</script>

<style>
.submit-form {
  max-width: 300px;
  margin: auto;
}
</style>



