<template>
  <div class="tabler">
    <tabler2-section>
      <template v-slot:1 name="col 1">test</template>
      <template v-slot:2 name="col 2">test 2</template>
    </tabler2-section>
    <div></div>
  </div>
</template>

<script>

import Tabler2Section from "./Tabler2Section";
export default {
  name: 'Tabler2',
  components: {Tabler2Section},
  props: {
    values: Array
  },
}
</script>

<style scoped>
  .tabler {
    display: table;
  }
</style>