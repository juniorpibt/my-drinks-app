<template>
  <div id="app">
    <SearchBar v-model:query="query" />
    <div class="stats">
      <span>🍹 Total Drinks: {{ totalDrinks }}</span>
    </div>
    <h1>Popular Drinks</h1>
    <DrinkList :query="query" @update-total-drinks="updateTotalDrinks" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import SearchBar from './components/SearchBar.vue';
import DrinkList from './components/DrinkList.vue';

export default defineComponent({
  name: 'App',
  components: {
    SearchBar,
    DrinkList
  },
  setup() {
    const query = ref('');
    const totalDrinks = ref(0);

    const updateTotalDrinks = (count: number) => {
      totalDrinks.value = count;
    };

    return {
      query,
      totalDrinks,
      updateTotalDrinks
    };
  }
});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

#app {
  font-family: 'Roboto', sans-serif;
  text-align: center;
  color: #fff;
  background-color: #2c3e50;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  max-width: 1200px;
  margin: 0 auto;
}

.stats {
  display: flex;
  justify-content: center;
  gap: 15px;
  margin-bottom: 20px;
  font-size: 1.1rem;
}

h1 {
  font-size: 2.5rem;
  margin: 20px 0;
  color: #ecf0f1;
}

/* Adicione as regras de mídia aqui */
@media (min-width: 768px) {
  #app {
    padding: 40px;
  }

  h1 {
    font-size: 3rem;
  }

  .stats {
    font-size: 1.3rem;
  }
}

@media (min-width: 1024px) {
  .DrinkList {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  }

  .drink {
    max-width: 250px;
  }

  .drink-title {
    font-size: 1.5rem;
  }

  p {
    font-size: 1.1rem;
  }
}
</style>
