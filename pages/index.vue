<template>
  <div class="content">
    <appForm/>
  </div>
</template>

<script>
import home from "~/content/home.json";

import appForm from "~/components/Form.vue";
export default {
  components: {
    appForm
  }
};
</script>

<style scoped lang="scss">
.pin-container {
  position: absolute;
  &-r {
    right: 4rem;
  }
}
</style>
