<template>
  <div class="p-8 pb-0 text-orange-500">
    <h1 class="text-4xl font-bold mb-4">Random Meals</h1>
  </div>
  <Meals :meals="meals" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import Meals from "../components/Meals.vue";
import axiosClient from "../axiosClient.js";

const meals = ref([]);

onMounted(async () => {
  for (let i = 0; i < 12; i++) {
    const { data } = await axiosClient.get(`random.php`);
    meals.value.push(data.meals[0]);
    // Trigger Vue reactivity
    meals.value = [...meals.value];
  }
});
</script>
