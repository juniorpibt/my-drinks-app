<template>
  <div class="SearchBar">
    <input v-model="internalQuery" placeholder="Search for a cocktail..." />
  </div>
</template>

<script lang="ts">
import { defineComponent, computed } from 'vue';

export default defineComponent({
  name: 'SearchBar',
  props: {
    query: {
      type: String,
      required: true
    }
  },
  emits: ['update:query'],
  setup(props, { emit }) {
    const internalQuery = computed({
      get: () => props.query,
      set: (value: string) => emit('update:query', value)
    });

    return {
      internalQuery
    };
  }
});
</script>

<style scoped>
.SearchBar {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.SearchBar input {
  width: 100%;
  max-width: 500px;
  padding: 10px 15px;
  border-radius: 25px;
  border: 1px solid #34495e;
  background-color: #ecf0f1;
  color: #2c3e50;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: border-color 0.3s ease;
}

.SearchBar input:focus {
  border-color: #3498db;
  outline: none;
}
</style>
