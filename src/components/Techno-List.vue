<template>
  <h3>Toutes les technos à veiller</h3>
  {{technos.length}} techno{{technos.length > 1 ? 's' : ''}}
  <ul>
    <li v-for="tech in technos" :key="tech.id">
      <button @click="editTechno(tech)">modif</button>
      <button @click="deleteTechno(tech)">suppr</button>
      <span v-if="technoToEdit !== null && technoToEdit.id === tech.id">
        <input type="text" v-model="technoToEdit.techno" @keypress.enter="save" />
        <button @click="save">sauvegarder</button>
      </span>
      <span v-else>{{tech.techno}}</span>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";
export default {
  emits: ["delete-techno", "edit-techno"],
  setup(props, { emit }) {
    let technoToEdit = ref(null);
    let deleteTechno = function (tech) {
      emit("delete-techno", tech);
    };

    let editTechno = function (tech) {
      technoToEdit.value = tech;
      console.log("TechnoList | technoToEdit()", technoToEdit);
    };

    let save = function () {
      emit("edit-techno", technoToEdit.value);
      technoToEdit.value = null;
    };

    return {
      deleteTechno,
      technoToEdit,
      editTechno,
      save,
    };
  },
  props: {
    technos: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
ul {
  text-align: left;
  width: 50%;
  margin-left: 100px;
}
</style>