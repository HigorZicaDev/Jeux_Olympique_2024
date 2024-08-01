<script setup>

import { onMounted, reactive } from "vue";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import NotImage from "@/assets/img/not-image.svg";
import Gold from "@/assets/img/medal-gold.svg";
import Silver from "@/assets/img/medal-silver.svg";
import Bronze from "@/assets/img/medal-bronze.svg";
import MedalTotal from "@/assets/img/medal-total.svg";


const state = reactive({
        countries: [],
        isLoading: true
    });

onMounted(async () => {

  try {
    const response = await fetch("https://apis.codante.io/olympic-games/countries");
    const obj = await response.json();
    state.countries = obj.data;
    // console.log(obj.data);
    state.countries.sort((function (x,y) {
      if(x.rank_total_medals !== 0){
        return x.rank_total_medals - y.rank_total_medals
      }

    }))
    console.log(state.countries);
  } catch (error) {
    console.error(error);
  } finally {
    state.isLoading = false;
  }

});

</script>

<template>
  <div class="p-4">
    <div class="container-xl lg:container m-auto">
        <div v-if="state.isLoading" class="text-center text-gray-500 py-6">
            <PulseLoader />
        </div>
        <div v-else class="grid grid-cols-1 md:grid-cols-4 gap-6">
          <div v-for="country in state.countries" :key="country.id" class="max-w-sm rounded overflow-hidden shadow-lg">
            <img class="w-full object-cover object-center" v-bind:src="country.flag_url" alt="Sunset in the mountains">
            <div class="px-6 py-4">
              <div class="font-bold text-xl mb-2">{{ country.name }}</div>
    
            </div>
            <div class="px-6 pt-4 pb-2">
              <span class="flex bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">
                <img v-bind:src="Gold" alt="Medal Gold" width="35" height="35">
                <span class="mt-2">{{ country.gold_medals }} médailles</span>
              </span>
              <span class="flex bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">
                <img v-bind:src="Silver" alt="Medal Silver" width="35" height="35">
                <span class="mt-2">{{ country.silver_medals }} médailles</span>
              </span>
              <span class="flex bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">
                <img v-bind:src="Bronze" alt="Medal Bronze" width="35" height="35">
                <span class="mt-2">{{ country.bronze_medals }} médailles</span>
              </span>
              <span class="flex bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">
                <img v-bind:src="MedalTotal" alt="Medal Bronze" width="35" height="35">
                <span class="mt-2">Total: {{ country.total_medals }} médailles</span>
              </span>
            </div>
          </div>
    
    
        </div>
        
      </div>
    </div>
</template>
