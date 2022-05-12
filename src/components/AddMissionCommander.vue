<template>
  <div class="submit-form">
    <div v-if="!submitted">
    <h3>Nuevo Mission Commander</h3>
      <div class="form-group">
        <label for="title">Nombre</label>
        <input
          type="text"
          class="form-control"
          id="title"
          required
          v-model="missioncommander.name"
          name="title"
        />
      </div>
      <div class="form-group">
        <label for="title">Username</label>
        <input
          type="text"
          class="form-control"
          id="username"
          required
          v-model="missioncommander.username"
          name="username"
        />
      </div>
      <div class="form-group">
        <label for="title">Main Stack</label>
        <input
          type="text"
          class="form-control"
          id="mainStack"
          required
          v-model="missioncommander.mainStack"
          name="mainStack"
        />
      </div>
      <div class="form-group">
        <label for="title">Current Enrollments</label>
        <input
          type="text"
          class="form-control"
          id="currentEnrollments"
          required
          v-model="missioncommander.currentEnrollments"
          name="currentEnrollments"
        />
      </div>
      <div class="form-group">
        <label for="title">Azure Certification</label>
        <input
          type="text"
          class="form-control"
          id="hasAzureCertification"
          required
          v-model="missioncommander.hasAzureCertification"
          name="hasAzureCertification"
        />
      </div>
      <button @click="saveMissionCommander" class="btn btn-success">Agregar</button>
    </div>
    <div v-else>
      <h4> Mission Commander creado exitosamente. </h4>
      <button class="btn btn-success" @click="newMissionCommander">Add</button>
    </div>
  </div>
</template>

<script>
import missionCommanderService from "../services/missionCommanderService";
export default {
  name: "add-missioncommander",
  data() {
    return {
      missioncommander: {
        id: null,
        name: "",
        username: "",
        mainStack: "",
        currentEnrollments: "",
        hasAzureCertification: ""
      },
      submitted: false
    };
  },
  methods: {
    saveMissionCommander() {
      var data = {
        name: this.missioncommander.name,
        username: this.missioncommander.username,
        mainStack: this.missioncommander.mainStack,
        currentEnrollments: (this.missioncommander.currentEnrollments === 'true'),
        hasAzureCertification: (this.missioncommander.hasAzureCertification === 'true')
      };
      missionCommanderService.create(data)
        .then(response => {
          this.missioncommander.id = response.data.id;
          this.submitted = true;
        })
        .catch(e => {
          console.log(e);
      });
    },
    newMissionCommander() {
      this.submitted = false;
      this.missioncommander = {};
    }
  }
};
</script>
