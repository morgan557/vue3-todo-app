<template>
  <h1>Veille techno</h1>
  <Form @add="saveTechno" />
  <br />
  <TechnoList :technos="technos" @delete-techno="deleteTechno" @edit-techno="editTechno" />
</template>

<script>
import { ref } from "vue";
import Form from "@/components/Form";
import TechnoList from "@/components/Techno-List";
export default {
  name: "App",
  components: {
    Form,
    TechnoList,
  },
  setup() {
    let technos = ref([]);

    const saveTechno = function (data) {
      console.log("App / saveTechno()", data);
      technos.value = [...technos.value, { techno: data, id: Date.now() }];
      console.log("technos", technos);
    };

    const editTechno = function (data) {
      technos.value = technos.value.map((t) => (t.id !== data.id ? t : data));
    };

    const deleteTechno = function (tech) {
      console.log("App / deleteTechno()", tech);
      technos.value = technos.value.filter((t) => t.id !== tech.id);
    };

    return {
      saveTechno,
      editTechno,
      deleteTechno,
      technos,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul {
  list-style: none;
}
</style>
