<template>
  <div class="filters">
    <button
      class="filter"
      :class="{ active: filter == 'all' }"
      @click="setFilter('all')"
    >
      All
    </button>
    <button
      class="filter"
      :class="{ active: filter == 'active' }"
      @click="setFilter('active')"
    >
      Active
    </button>
    <button
      class="filter"
      :class="{ active: filter == 'completed' }"
      @click="setFilter('completed')"
    >
      Completed
    </button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "filters",
  props: { filter: { type: String, required: true } },
  methods: {
    setFilter(filter: string) {
      this.$emit("setFilter", filter);
    }
  }
});
</script>

<style scoped lang="scss">
.filters {
  display: flex;
  justify-content: flex-start;
  padding: 16px 0;
  border-top: 1px solid #ccc;
}

.filter {
  background: #35495e;
  border-radius: 8px;
  margin-right: 16px;
  padding: 8px;
  font-weight: bold;
  font-size: 14px;
  color: #fff;
}

.active {
  background: #42b883;
}
</style>
