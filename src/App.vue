<script setup lang="ts">
import { ref } from "vue";

const episodeName = ref<string>("Cheaty Cheaty Bang Bang");
const randomEpisode = ref<string>("Season #13, Episode #11");

// TODO: generate link to episode description? Maybe wiki?
</script>

<template>
  <main class="container mx-auto flex flex-col justify-center items-center">
    <h1 class="text-6xl mb-6 text-red-400">Bob's Burgers</h1>
    <h1 class="text-5xl mt-6 mb-2 text-red-400 uppercase font-medium">
      Episode
    </h1>
    <h1 class="text-3xl mb-6 text-red-400 uppercase">of the Day</h1>

    <div
      class="border-3 border-blue-400 p-8 mt-6 w-md flex flex-col justify-center items-center"
    >
      <h2 class="text-2xl text-red-400 mb-2" v-if="randomEpisode">
        "{{ episodeName }}"
      </h2>
      <h2 class="text-xl text-red-400" v-if="randomEpisode">
        {{ randomEpisode }}
      </h2>
    </div>
    <button
      id="random-episode-btn"
      class="w-xs text-white p-2 px-4 text-xl font-semibold bg-blue-400 mt-8"
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
