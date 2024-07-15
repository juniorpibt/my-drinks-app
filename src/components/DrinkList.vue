<template>
  <div class="DrinkList">
    <DrinkItem v-for="drink in filteredDrinks" :key="drink.idDrink" :drink="drink" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed, onMounted } from 'vue';
import axios from 'axios';
import DrinkItem from './DrinkItem.vue';

export default defineComponent({
  name: 'DrinkList',
  components: {
    DrinkItem
  },
  props: {
    query: {
      type: String,
      required: true
    }
  },
  emits: ['update-total-drinks'],
  setup(props, { emit }) {
    const drinks = ref([]);

    const fetchDrinks = async () => {
      try {
        const response = await axios.get('https://www.thecocktaildb.com/api/json/v1/1/search.php?s=');
        drinks.value = response.data.drinks;
        emit('update-total-drinks', drinks.value.length);
      } catch (error) {
        console.error('Error fetching drinks:', error);
      }
    };

    onMounted(() => {
      fetchDrinks();
    });

    const filteredDrinks = computed(() => {
      return drinks.value.filter(drink =>
        drink.strDrink.toLowerCase().includes(props.query.toLowerCase())
      );
    });

    return {
      filteredDrinks
    };
  }
});
</script>

<style scoped>
.DrinkList {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
  justify-items: center;
  margin-top: 20px;
}
</style>
