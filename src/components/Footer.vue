<template>
  <div class="footer">
    <div>{{ remaining }} items left</div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "footer",
  props: { remaining: { type: Number, required: true } },
});
</script>

<style scoped lang="scss">
.footer {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-top: 16px;
  padding: 16px 0;
  border-top: 1px solid #ccc;
  font-size: 14px;
}
</style>