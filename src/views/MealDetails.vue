<template>
  <div class="meal-details-container">
    <div class="grid-container">
      <div class="meal-image-container">
        <img :src="meal.strMealThumb" :alt="meal.strMeal" class="meal-image">
      </div>
      <div class="meal-details">
        <h1 class="meal-title">{{ meal.strMeal }}</h1>

        <div class="meal-info">
          <div class="info-item">
            <strong class="info-label">Category:</strong> {{ meal.strCategory }}
          </div>
          <div class="info-item">
            <strong class="info-label">Area:</strong> {{ meal.strArea }}
          </div>
          <div class="info-item">
            <strong class="info-label">Tags:</strong> {{ meal.strTags }}
          </div>
        </div>
      </div>
    </div>
    <div class="meal-instructions">
        {{ formattedInstructions }}
    </div>
    <div class="ingredients-and-external-links">
      <div class="ingredients">
        <h2 class="section-title">Ingredients</h2>
        <ul class="capitlize">
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strIngredient${ind + 1}`]">
              &bull; {{ meal[`strMeasure${ind + 1}`] }} {{ meal[`strIngredient${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>

      <div class="external-links">
        <YouTubeButton :href="meal.strYoutube" />
        <a
          :href="meal.strSource"
          target="_blank"
          class="source-link"
        >
          View Original Source
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, computed } from 'vue'
import { useRoute } from 'vue-router';
import axiosClient from '../axiosClient';
import YouTubeButton from '../components/YouTubeButton.vue';

const route = useRoute();
const meal = ref({})

const formattedInstructions = computed(() => {
  if (meal.value.strInstructions) {
    return meal.value.strInstructions.replace(/\./g, '.\n');
  }
  return '';
});

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`)
    .then(({ data }) => {
      meal.value = data.meals[0] || {}
    })
})

</script>

<style scoped>
/* Regular CSS styles */
.meal-details-container {
  font-family: 'Roboto';
  max-width: 800px;
  margin: 0 auto;
  padding: 8px;
}

.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.meal-image-container {
  max-width: 100%;
  max-height: 100%;
  overflow: hidden;
  border-radius: 8px; /* Rounded corners */
  transition: transform 0.3s ease, box-shadow 0.3s ease; /* Transition for transform and box-shadow */
}

.meal-image-container:hover {
  transform: scale(1.05); /* Zoom effect on hover */
}

.meal-image {
  width: 100%;
  height: auto;
  display: block;
  border-radius: 8px; /* Rounded corners */
}

.meal-details {
  border-radius: 8px; /* Rounded corners */
  background-color: #e7e5e5; /* Light gray background */
  padding: 1rem; /* Add padding for spacing */
  height: 100%;
  display: flex;
  flex-direction: column;
  transition: transform 0.3s ease, box-shadow 0.3s ease; /* Transition for transform and box-shadow */
}

.meal-details:hover {
  transform: scale(1.05); /* Zoom effect on hover */
}

.meal-title {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  color: #ff6600; /* Orange color */
}

.meal-info {
  font-size: 1.125rem; /* 18px */
  margin-top: 1rem;
}

.info-item {
  margin-bottom: 0.5rem;
}

.info-label {
  font-weight: bold;
}

.meal-instructions {
  margin-top: 1rem;
  border-radius: 8px; /* Rounded corners */
  background-color: #e7e5e5; /* Light gray background */
  padding: 1rem; /* Add padding for spacing */
  white-space: pre-line; /* Preserve line breaks */
}


.ingredients-and-external-links {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  margin-top: 20px;
}

.ingredients {
  grid-column: 1 / span 1;
}

.external-links {
  grid-column: 2 / span 1;
}

.section-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.external-links {
  margin-top: 1rem;
}

.source-link {
  display: inline-block;
  padding: 0.75rem;
  border: 2px solid transparent;
  border-radius: 4px;
  color: #4b0082; /* Indigo color */
  text-decoration: none;
  transition: border-color 0.3s ease;
}

.source-link:hover {
  border-color: #4b0082;
}

.capitlize{
  text-transform: capitalize;
}
</style>
