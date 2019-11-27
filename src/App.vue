<template>
  <div id="app">
    <p> Please input a valid number between 1-100 </p>
<input type="number" v-model="limit" min="0" max="100" oninput="validity.valid||(value='');"/><Numbers/>
  </div>
</template>

<script>
import Numbers from "@/components/Numbers";

export default {
  name: "App",
  components: { Numbers },
  data() {
    return {
      limit: 100
    };
  }
};
</script>

<style scoped>
</style>
