<template>
  <form @submit.prevent="addTechno">
    <label for="techno">Techno</label>
    <br />
    <input type="text" name="techno" v-model="techToLearn" />
    <br />
    <button type="submit">ajouter</button>
  </form>
</template>

<script>
import { ref } from "vue";
export default {
  setup(props, ctx) {
    let techToLearn = ref("");
    const addTechno = function () {
      console.log("techToLearn", techToLearn.value);
      ctx.emit("add", techToLearn.value);
      techToLearn.value = "";
    };

    return {
      techToLearn,
      addTechno,
    };
  },
};
</script>

<style>
</style>