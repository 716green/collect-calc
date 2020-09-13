<template>
  <div class="home">
    <img src="../assets/logo.svg" width="20%" />
    <Main title="Calculator" />
  </div>
</template>

<script>
import Main from "@/components/Main.vue";

export default {
  name: "Home",
  components: {
    Main,
  },
};
</script>
<style>
* {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
</style>