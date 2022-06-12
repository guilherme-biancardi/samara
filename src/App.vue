<template>
  <main class="content">
    <h1>Estamos juntos há...</h1>
    <ul class="counter-list">
      <li v-for="(count, index) in counter" :key="index" class="counter">
        <h2>{{ count.value.toLocaleString() }}</h2>
        <p>{{ count.label }}</p>
      </li>
      <li class="counter">
        <div class="music-text">
          <img src="./assets/music.svg" />
          <a :href="state.musicLink" target="_blank">Nossa música</a>
        </div>
      </li>
    </ul>
    <p>{{ state.information.text }} - {{ moment(date).format("DD-MM-YYYY") }}</p>
  </main>
</template>

<script setup>
import moment from "moment";
import { computed, reactive } from "vue";

const date = "2022-03-20 15:35:00";

const state = reactive({
  seconds: 0,
  momentCreated: moment(),
  musicLink: "https://www.youtube.com/watch?v=L5gMlsK2Gsc",
  information: {
    text: "Não tem jeito",
  },
});

const getDiff = (type) => state.momentCreated.diff(date, type);

const counter = computed(() => [
  { label: "anos", value: getDiff("years") },
  { label: "dias", value: getDiff("days") },
  { label: "minutos", value: getDiff("minutes") },
  { label: "segunodos", value: getDiff("seconds") },
]);

setInterval(() => (state.momentCreated = moment()), 1000);
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@200;400;500&family=Pacifico&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Inter", sans-serif;
}

ul {
  list-style: none;
}

h1 {
  font-family: "Pacifico", cursive;
  font-weight: 100;
  font-size: 1.8em;
}

.content {
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: white;
  width: 100%;
  height: 100vh;
  background: url("./assets/IMG_2589.jpg") no-repeat center;
  background-size: cover;
  row-gap: 8px;
}

.counter-list {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr;
  gap: 8px;
}

.counter {
  padding: 14px 20px;
  background: rgba(255, 255, 255, 0.15);
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(3.4px);
  text-align: center;
  font-size: 1em;
  min-width: 200px;
}

.counter p {
  text-transform: uppercase;
}

.music-text {
  display: flex;
  justify-content: center;
  align-items: center;
  column-gap: 8px;
}

.music-text a {
  font-family: "Pacifico", cursive;
  color: white;
  font-size: 1.2em;
}

.music-text img {
  min-width: 28px;
}

.content > p {
  font-family: "Pacifico", cursive;
}
</style>
