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
    <p>{{ state.information.text }} - {{ moment(date).format("DD/MM/YYYY") }}</p>
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
 { label: "horas", value: getDiff("hours") },
  { label: "minutos", value: getDiff("minutes") },
  { label: "segundos", value: getDiff("seconds") },
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
  font-size: clamp(0.5em, calc(0.75em + 1vw), 1.04em);
}

ul {
  list-style: none;
}

h1 {
  font-family: "Pacifico", cursive;
  font-weight: 100;
  font-size: 1.8em;
  color: #fff;
  text-shadow: 2px 2px 12px rgba(0, 0, 0, 0.75);
}

.content {
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #fff;
  width: 100%;
  height: 100vh;
  background: url("./assets/background.jpeg") no-repeat center;
  background-size: cover;
  row-gap: 8px;
}

.content h2{
  font-size: 1.2em;
  font-weight: 800;
}

.counter-list {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr;
  gap: 8px;
}

.counter {
  padding: 14px 20px;
  background: rgba(116, 116, 116, 0.4);
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(3.5px);
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
  color: #fff;
  font-size: 1.2em;
}

.music-text img {
  min-width: 28px;
}

.content > p {
  font-family: "Pacifico", cursive;
  text-shadow: 2px 2px 12px rgba(0, 0, 0, 0.75);
  font-size: 1.1em;
}
@media screen and (min-width: 1024px) {
  .counter-list{
    width: 40%;
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
