<template>  
  <div class="w-[800px] mx-auto">
    <h1 class="text-5xl font-bold mb-5">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" :alt="meal.strMeal" class="w-[100%]"/>
    <div class="grid grid-cols-1 sm:grid-cols-3 text-lg py-2">
      <div><strong>Category: </strong> {{ meal.strCategory }}</div>
      <div><strong>Area: </strong> {{ meal.strArea }}</div>
      <div><strong>Tags: </strong> {{ meal.strTags }}</div>
    </div>
    <div>
        {{ meal.strInstructions }}
    </div>
    <div class="grid grid-cols-1 sm:grid-cols-2">
        <div>
            <h2 class="text-2xl font-semibold mb-2">Ingredient</h2>
            <ul>
                <template v-for="(el, ind) of new Array(20)">
                    <li v-if="meal[`strIngredient${ind + 1}`]">
                        {{ ind+1 }}. {{ meal[`strIngredient${ind + 1}`] }}
                    </li>
                </template>                
            </ul>
        </div>
        <div>
            <h2 class="text-2xl font-semibold mb-2">Measures</h2>
            <ul>
                <template v-for="(el, ind) of new Array(20)">
                    <li v-if="meal[`strMeasure${ind + 1}`]">
                        {{ ind+1 }}. {{ meal[`strMeasure${ind + 1}`] }}
                    </li>
                </template>                
            </ul>
        </div>
        <div class="mt-4 mb-4">
            <YoutubeButton :href="meal.strYoutube"></YoutubeButton>
            <a
            :href="meal.strSource" 
            target="_blank" 
            class="ml-4 px-3 py-2 rounded text-white bg-cyan-600 hover:bg-cyan-700 transition-colors"
            >
                View Original Source
            </a>
        </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import YoutubeButton from '../components/YoutubeButton.vue';
import axiosClient from "../axiosClient";

const route = useRoute();
const meal = ref({});

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0] || {};
  });
});
</script>
