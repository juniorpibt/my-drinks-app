<template>
    <div class="drink" @click="toggleDescription">
      <img :src="drink.strDrinkThumb" alt="Drink Image" />
      <div class="drink-title">{{ drink.strDrink }}</div>
      <p v-if="showDescription">{{ drink.strInstructions }}</p>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent, ref } from 'vue';
  
  export default defineComponent({
    name: 'DrinkItem',
    props: {
      drink: {
        type: Object,
        required: true
      }
    },
    setup() {
      const showDescription = ref(false);
  
      const toggleDescription = () => {
        showDescription.value = !showDescription.value;
      };
  
      return {
        showDescription,
        toggleDescription
      };
    }
  });
  </script>
  
  <style scoped>
  .drink {
    background-color: #34495e;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    padding: 10px;
    width: 100%;
    max-width: 200px;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    cursor: pointer;
  }
  
  .drink:hover {
    transform: translateY(-5px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
  
  img {
    width: 100%;
    border-radius: 8px;
    margin-bottom: 10px;
  }
  
  .drink-title {
    font-size: 1.2rem;
    color: #ecf0f1;
  }
  
  p {
    font-size: 1rem;
    color: #bdc3c7;
  }
  
  </style>
  