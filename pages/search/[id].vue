<script setup lang="ts">
import { onMounted, ref } from "vue";

const route = useRoute();

const episodes = ref([]);

onMounted(async () => {
  const fetchData = await fetch(
    `https://api.tvmaze.com/shows/${route.params.id}?embed=episodes`
  );
  const json = await fetchData.json();
  episodes.value = json._embedded.episodes;
});

console.log("route", route.params.id);
</script>
<template>
  <div>
    <NuxtLink to="/">Go Back</NuxtLink>
    <div class="shows">
      <div class="show" v-for="episode in episodes" :key="episode.id">
        <div>
          {{ episode.name }}
        </div>
        <img :src="episode.image?.medium" alt="" />
      </div>
    </div>
  </div>
</template>
