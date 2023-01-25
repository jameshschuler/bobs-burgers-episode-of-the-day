<template>
  <main class="container mx-auto flex flex-col justify-center items-center">
    <h1 class="text-6xl mb-6 text-red-400">Bob's Burgers</h1>
    <h1 class="text-5xl mt-6 mb-2 text-red-400 uppercase font-medium">
      Episode
    </h1>
    <h1 class="text-3xl mb-6 text-red-400 uppercase">of the Day</h1>

    <div
      class="border-3 border-blue-400 p-8 mt-6 min-w-md w-auto flex flex-col justify-center items-center"
    >
      <a
        class="text-2xl text-red-400 mb-2"
        :href="episodeWikiUrl"
        target="_blank"
        v-if="episodeName"
      >
        {{ episodeName }}
      </a>
      <h2 class="text-xl text-red-400" v-if="seasonEpisodeText">
        {{ seasonEpisodeText }}
      </h2>
    </div>
    <button
      id="random-episode-btn"
      class="w-xs text-white p-2 px-4 text-xl font-semibold bg-blue-400 mt-8"
      @click="getRandomEpisode()"
    >
      Random
      <span><i class="fa-solid fa-burger mx-1"></i></span>
      Episode
    </button>
  </main>
  <footer class="py-6">
    <div class="flex justify-center flex-col items-center">
      <p class="mb-3">
        Made with <i class="fas fa-fw fa-heart text-red-500"></i> by
        <a href="https://jamesschuler.io" target="_blank">James Schuler</a>.
      </p>
      <p>
        <a
          href="https://github.com/jameshschuler/doug-score-viewer"
          target="_blank"
          ><i class="fab fa-fw fa-lg fa-github-alt"></i
        ></a>
      </p>
    </div>
  </footer>
</template>
<script setup lang="ts">
import { onMounted, ref } from "vue";

const episodeName = ref<string>();
const episodeWikiUrl = ref<string>();
const seasonEpisodeText = ref<string>();
const totalEpisodeCount = ref<number>(1);

const baseUrl = "https://bobsburgers-api.herokuapp.com";

const getRandomNumber = (min: number, max: number) =>
  Math.floor(Math.random() * (max - min)) + min;

async function getRandomEpisode() {
  const randomEpisodeNumber = getRandomNumber(1, totalEpisodeCount.value + 1);

  const response = await fetch(`${baseUrl}/episodes/${randomEpisodeNumber}`);
  const { episode, episodeUrl, name, season } = await response.json();

  episodeName.value = name;
  episodeWikiUrl.value = episodeUrl;
  seasonEpisodeText.value = `Season #${season}, Episode #${episode}`;
}

async function getTotalEpisodes() {
  const response = await fetch(`${baseUrl}/episodes`);
  const data = await response.json();
  totalEpisodeCount.value = data.length;
}

onMounted(async () => {
  await getTotalEpisodes();
  await getRandomEpisode();
});
</script>
<style lang="scss">
* {
  font-family: "Poppins", sans-serif;
}

html,
body {
  width: 100%;
  height: 100%;
  background-color: hsl(48, 96%, 89%);
}
html {
  scroll-behavior: smooth;
}
@media screen and (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}

#app {
  min-height: 100%;
  display: flex;
  flex-direction: column;
  align-items: stretch;

  main {
    flex-grow: 1;

    #random-episode-btn {
      &:hover {
        background-color: hsl(217, 91%, 60%);
      }
    }
  }

  main,
  footer {
    flex-shrink: 0;
  }
}
</style>
