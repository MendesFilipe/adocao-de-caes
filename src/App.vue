<template>
<div id="app">
  <dogForm />
</div>
</template>
<script>
import dogForm from "@/views/dogForm";

export default {
  name: "app",
  components: {
    dogForm
  }
};
</script>
<style scoped>
#app {
  display: inline;
  background: #56CCF2;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #2F80ED, #56CCF2);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to right, #2F80ED, #56CCF2); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
</style>
